<template>
  <div>
    <Masthead>
      <h1>ISYF 2025</h1>
    </Masthead>

    <main>
      <div class="picture-viewer-wrapper" :class="{ shown: viewerShown }" @click="viewerShown = false">
        <button class="controls picture-back" @click.stop="adjustPhotoIndex(-1)"
          :class="{ enabled: getPhotoOffsetAvailable(-1) }">
          <span class="material-icons-outlined"> chevron_left </span>
        </button>
        <div class="loading_icon" id="loading_icon"></div>
        <img id="picture" :style="{ height: photoHeight + 'px', width: photoWidth + 'px' }"
          :src="photos[currentDay - 1][currentPhotoId].replace('.webp', '').replace('small', 'big')" @click.stop=""
          @load="onImageLoad()" />
        <button class="controls picture-forwards" @click.stop="adjustPhotoIndex(1)"
          :class="{ enabled: getPhotoOffsetAvailable(1) }">
          <span class="material-icons-outlined"> chevron_right </span>
        </button>
      </div>

      <section class="live-pictures">
        <div class="days-wrapper-wrapper">
          <div class="days-wrapper">
            <div class="days">
              <button class="day" :class="{ selected: day == currentDay }" :style="{ '--day': currentDay }"
                v-for="day in totalDays" @click="changeDay(day)">
                Day {{ day - 1 }}
              </button>
            </div>
          </div>
        </div>
        <div class="slider" :class="{ loading: sliderLoading }">
          <div class="slide" v-for="(link, photoId) in photos[currentDay - 1]" @click="showImage(photoId)"
            v-if="photos[currentDay - 1].length > 0">
            <img :src="link" />
          </div>
          <div class="slider-empty" v-else>
            <img src="/public/event_images/shrug.webp">
            <span>Sorry, nothing available yet!</span>
          </div>
        </div>
      </section>
      <span>Link to photos on Google Drive: <a class="a_no_underline" href="https://drive.google.com/drive/folders/1p4cfXtDtIjeNj6zNjYKUDXM_vQ2JjXDQ">https://drive.google.com/drive/folders/1p4cfXtDtIjeNj6zNjYKUDXM_vQ2JjXDQ</a></span>
    </main>
  </div>
</template>

<style>
.a_no_underline {
  text-decoration: none;
  color: var(--primary);
}
.masthead::before {
  color: var(--bg);
  background-image: url("/images/mediabg.webp");
  filter: brightness(40%);
  background-size: cover;
  background-repeat: no-repeat;
  background-position: 43% 50%;
}

#body#body {
  max-width: none;
}
</style>

<style scoped>
.live-pictures {
  border-radius: 8px;
  border: 1px solid var(--fg);
}

.days-wrapper-wrapper {
  position: sticky;
  top: 3.5rem;
  width: calc(100% + 2px);
  z-index: 10;
  background-color: var(--bg);
  margin: -1px;
  margin-top: calc(-0.5rem - 1px);
  padding-top: 0.75rem;
}

.days-wrapper {
  border: 1px solid var(--fg);
  background-color: none;
  border-radius: 8px 8px 0 0;
  overflow-x: auto;
}

.days {
  --tab-width: 7rem;

  display: flex;
  height: 3rem;
  width: fit-content;
  justify-content: center;
  align-items: center;

  font-family: var(--font-display);
  font-weight: bold;
  font-size: 22px;
  color: var(--gray-300);
  border-radius: 8px 8px 0 0;
}

.day {
  transition: color 100ms;
  position: relative;
  height: 100%;
  width: var(--tab-width);
}

.day:hover {
  color: var(--primary);
}

.day.selected {
  color: var(--primary);
}

.day:first-of-type::before {
  content: "";
  position: absolute;
  inset: 0;
  z-index: -1;
  background-color: var(--primary-100);
}

.day:first-of-type::after {
  content: "";
  z-index: 10;
  position: absolute;
  left: 0;
  right: 0;
  top: calc(100% - 3px);
  height: 3px;
  border-radius: 2px;
  background-color: var(--primary);
}

.day:first-of-type::before,
.day:first-of-type::after {
  transform: translateX(calc((var(--day) - 1) * var(--tab-width)));
  transition: transform 100ms;
}

/*
*
*
*
*/

.slider {
  position: relative;
  display: grid;
  place-items: center;
  overflow: hidden;
  grid-template-columns: repeat(auto-fit,
      minmax(clamp(18vw, 14rem, 44vw), 1fr));
  padding-top: 1rem;
  gap: 0.5rem;

  border-radius: 0 0 8px 8px;
  border-top: 1px solid var(--fg);
  --clr-1: var(--primary-900);
  --clr-2: var(--primary-950);
  --stripe-width: 8px;
  background-color: white;
}

.slider-empty {
  margin-block: 3rem;
}

.slider-empty img {
  max-width: 16rem;
}

.slider-empty span {
  display: block;
  margin-top: 2rem;
  text-align: center;
}

.slider::before {
  content: '';
  position: absolute;
  inset: 0;
  z-index: 100;
  background-color: transparent;
  visibility: hidden;
  transition: background-color 200ms, visibility 200ms;
}

.slider.loading::before {
  background-color: hsla(var(--bg-hsla), 0.9);
  visibility: visible;
}

.slide {
  /* height: 100%; */
  transition: transform 1s;
  position: relative;
}

.slide img {
  object-fit: contain;
  width: 100%;
  max-height: 10rem;
  margin-bottom: -4px;
  transition: filter 200ms;
}

.slide img:hover {
  filter: brightness(0.8);
}

/*
*
*
*
*/

.picture-viewer-wrapper {
  position: fixed;
  inset: 0;
  background-color: #000000dd;
  z-index: 200;
  display: grid;
  place-items: center;

  opacity: 0;
  visibility: hidden;
  transition: 200ms opacity, 200ms visibility;
}

.picture-viewer-wrapper.shown {
  opacity: 1;
  visibility: visible;
}

.loading_icon {
  display: none;
  width: 80px;
  height: 80px;
  position: absolute;
  border: 2px solid var(--bg);
  top: 50%;
  left: 50%;
  border-color: transparent var(--bg) transparent var(--bg);
  border-radius: 50%;
  animation: loader 1s linear infinite;
}

@keyframes loader {
  0% {
    transform: translate(-50%, -50%) rotate(0deg);
  }

  100% {
    transform: translate(-50%, -50%) rotate(360deg);
  }
}

.picture-viewer {
  width: 100% !important;
  /* height: 100% !important; */
}

#picture {
  border-radius: 8px;
  border: 1px solid var(--bg);
  box-sizing: border-box;
}

.controls {
  position: absolute;
  --fg: var(--bg);
  width: 4rem;
  height: 4rem;
  border-radius: 2rem;
  border: 1px solid var(--gray-100);
  display: grid;
  place-items: center;
  touch-action: manipulation;
  user-select: none;

  background-color: var(--gray-400);
}

.controls.enabled {
  background-color: var(--primary);
}

@media screen and (max-width: 600px) {

  .picture-back,
  .picture-forwards {
    bottom: 4rem;
  }

  .picture-back {
    left: calc(50vw - 6rem);
  }

  .picture-forwards {
    right: calc(50vw - 6rem);
  }
}

@media screen and (min-width: 600px) {
  .picture-back {
    left: max(calc(5vw - 2rem), 0.75rem);
  }

  .picture-forwards {
    right: max(calc(5vw - 2rem), 0.75rem);
  }
}
</style>

<script setup>
import { ref, nextTick, watch, onMounted, onUnmounted } from "vue";

const totalDays = 6;
const currentDay = ref(1);
const sliderLoading = ref(false)

const viewerShown = ref(false);
const currentPhotoId = ref(0);
const photoWidth = ref(0);
const photoHeight = ref(0);

function showImage(pictureId) {
  if (pictureId != currentPhotoId.value) {
    document.getElementById("picture").style.display = "none";
    document.getElementById("loading_icon").style.display = "block";

  }
  currentPhotoId.value = pictureId;
  viewerShown.value = true;
  setTimeout(resizePhoto, 1);
}
function getPhotoOffsetAvailable(offset) {
  return (
    currentPhotoId.value + offset >= 0 &&
    currentPhotoId.value + offset <= photos[currentDay.value - 1].length - 1
  );
}
function adjustPhotoIndex(offset) {
  //Should only be 1 or -1
  if (!getPhotoOffsetAvailable(offset)) return;
  currentPhotoId.value = currentPhotoId.value + offset;
  document.getElementById("picture").style.display = "none";
  document.getElementById("loading_icon").style.display = "block";
  setTimeout(resizePhoto, 1);
  // document.getElementById("picture").setAttribute("style", "width:photoWidth;height:photoHeight;");
}

function onImageLoad() {
  document.getElementById("picture").style.display = "block";
  document.getElementById("loading_icon").style.display = "none";
};

onMounted(() => {
  window.addEventListener("resize", resizePhoto);
  document.addEventListener("keydown", keyWatcher);
});
onUnmounted(() => {
  window.removeEventListener("resize", resizePhoto);
  document.removeEventListener("keydown", keyWatcher);
});
watch(currentPhotoId, setTimeout(resizePhoto, 10));

function keyWatcher(e) {
  if (!viewerShown.value) return;

  if (e.code == "ArrowLeft" || e.code == "ArrowUp" || e.code == "Backspace")
    adjustPhotoIndex(-1);
  else if (
    e.code == "ArrowRight" ||
    e.code == "ArrowDown" ||
    e.code == "Enter" ||
    e.code == "Space"
  )
    adjustPhotoIndex(1);
  else if (e.code == "Escape") viewerShown.value = false;
}

function changeDay(newDay) {
  sliderLoading.value = true
  currentDay.value = newDay
  setTimeout(() => {
    sliderLoading.value = false
  }, 750)
}

function resizePhoto() {
  const img = document.getElementById("picture");
  img.onload = function () {
    const height = img.naturalHeight;
    const width = img.naturalWidth;
    const scale = Math.min(
      (window.innerHeight * 0.9) / height,
      (window.innerWidth * 0.9) / width
    );
    photoHeight.value = height * scale;
    photoWidth.value = width * scale;
  }
}

function fetchPhotos() {
  // Fetch photos from images folder
  // Glob imports have to be static :eyeroll: so i have to statically import each one 
  let gallery = []
  gallery.push(Object.keys(import.meta.glob(`/public/event_images/small/day0/*.{png,jpg,jpeg,webp,PNG,JPEG,WEBP}`, { eager: true })).map(filePath => '/event_images/small/day0/' + filePath.split('/').pop()));
  gallery.push(Object.keys(import.meta.glob(`/public/event_images/small/day1/*.{png,jpg,jpeg,webp,PNG,JPEG,WEBP}`, { eager: true })).map(filePath => '/event_images/small/day1/' + filePath.split('/').pop()));
  gallery.push(Object.keys(import.meta.glob(`/public/event_images/small/day2/*.{png,jpg,jpeg,webp,PNG,JPEG,WEBP}`, { eager: true })).map(filePath => '/event_images/small/day2/' + filePath.split('/').pop()));
  gallery.push(Object.keys(import.meta.glob(`/public/event_images/small/day3/*.{png,jpg,jpeg,webp,PNG,JPEG,WEBP}`, { eager: true })).map(filePath => '/event_images/small/day3/' + filePath.split('/').pop()));
  gallery.push(Object.keys(import.meta.glob(`/public/event_images/small/day4/*.{png,jpg,jpeg,webp,PNG,JPEG,WEBP}`, { eager: true })).map(filePath => '/event_images/small/day4/' + filePath.split('/').pop()));
  gallery.push(Object.keys(import.meta.glob(`/public/event_images/small/day5/*.{png,jpg,jpeg,webp,PNG,JPEG,WEBP}`, { eager: true })).map(filePath => '/event_images/small/day5/' + filePath.split('/').pop()));

  return gallery
}
const photos = fetchPhotos()


definePageMeta({
  layout: "masthead",
});

// Loads high resolutions images in the background for quicker opening on demand
// Removed since this involves transferring a very large amount of data, which could be a concern for mobile data and roaming plan users
// photos.flat().forEach(url => {
//   const link = document.createElement("link");
//   link.rel = "prefetch";
//   link.href = url.replace(".webp", "").replace("small", "big");
//   document.head.appendChild(link);
// });
</script>
