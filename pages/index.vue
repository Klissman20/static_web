<template>
  <div class="relative min-h-screen">
    <div
      :class="100 <= progressBar ? 'opacity-0 scale-0' : 'opacity-50'"
      class="border-4 text-xl font-semibold z-10 bottom-1/2 left-1/2 absolute animate-spin w-9 h-9 shadow-lg border-green-700 bg-gray-300 rounded-2xl duration-100 ease"
    >
      -°
    </div>
    <img
      :class="100 <= progressBar || 'opacity-50 blur-sm'"
      class="relative z-0 duration-150 ease-in-out"
      :src="img"
      alt=""
    />
    <hr />
    <!--  -->
    <div
      :style="`width: ${progressBar}%;`"
      class="duration-75 ease h-2 bg-green-600"
    ></div>
    <button @click="loadImage">reload</button>
  </div>
</template>
<script setup>
const random = () => Math.random();
const img = ref("");
const load = ref(true);
const progressBar = ref(0);
let request;
onMounted(() => {
  /* var myImage = new Image();
  myImage.src ="https://picsum.photos/200/300?" + random();
  myImage.onprogress = (e) => {
    console.log(e.lengthComputable);
  }
  myImage.onload = (e) => {

    img.value = myImage.src;
    load.value = false;
  }; */
  loadImage();
});
function loadImage() {
  const imageURI = "https://picsum.photos/968/764?" + random();
  request = new XMLHttpRequest();
  request.onprogress = updateProgressBar;
  request.onload = showImage;
  request.open("GET", imageURI, true);
  request.overrideMimeType("text/plain; charset=x-user-defined");
  request.send(null);
}
function showImage() {
  //var myImage = new Image();
  //myImage.src = "data:image/jpeg;base64," + base64Encode(request.responseText);
  img.value = "data:image/jpeg;base64," + base64Encode(request.responseText);
}
function updateProgressBar({ lengthComputable, loaded, total }) {
  progressBar.value = lengthComputable ? Math.round((loaded / total) * 100) : 0;
}
function base64Encode(inputStr) {
  let b64 = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/=";
  let outputStr = "";
  let i = 0;

  while (i < inputStr.length) {
    //all three "& 0xff" added below are there to fix a known bug
    //with bytes returned by xhr.responseText
    let byte1 = inputStr.charCodeAt(i++) & 0xff;
    let byte2 = inputStr.charCodeAt(i++) & 0xff;
    let byte3 = inputStr.charCodeAt(i++) & 0xff;

    let enc1 = byte1 >> 2;
    let enc2 = ((byte1 & 3) << 4) | (byte2 >> 4);

    let enc3, enc4;
    if (isNaN(byte2)) {
      enc3 = enc4 = 64;
    } else {
      enc3 = ((byte2 & 15) << 2) | (byte3 >> 6);
      if (isNaN(byte3)) {
        enc4 = 64;
      } else {
        enc4 = byte3 & 63;
      }
    }

    outputStr +=
      b64.charAt(enc1) + b64.charAt(enc2) + b64.charAt(enc3) + b64.charAt(enc4);
  }

  return outputStr;
}
</script>
