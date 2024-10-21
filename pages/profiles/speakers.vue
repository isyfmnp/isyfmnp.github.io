<template>
  <h1>Invited Speakers</h1>

  <p>
    Click on each speakers name to see their profile! You can also scroll down and see
    further details
  </p>

  <div class="collage">
    <section
      class="event"
      v-for="(event, eventIndex) in profiles"
      :class="{'event-open': eventsOpen[eventIndex]}"
    >
      <h3 class="event-title">{{ event.event }}</h3>
      <a
        class="profile"
        v-for="profile in event.profiles"
        :href="'#' + profile.name.replaceAll(' ', '')"
        @click="resetLink"
      >
        <img
          class="profile-img"
          :src="'/images/profiles/speakers/' + profile.image + '_square.jpg'"
          alt=""
        />
        <div class="name">
          {{ profile.name }}
        </div>
      </a>
    </section>
  </div>

  <div class="intros">
    <div class="event" v-for="event in profiles">
      <h2>
        <div class="scroll-banner-wrapper">
          <span class="scroll-banner">{{
            event.event.concat('&nbsp;&nbsp;•&nbsp;&nbsp;').repeat(30)
          }}</span>
        </div>
      </h2>

      <section class="profile" v-for="profile in event.profiles">
        <div class="scroll-anchor" :id="profile.name.replaceAll(' ', '')"></div>
        <img
          :src="'/images/profiles/speakers/' + profile.image + '.jpg'"
          :alt="profile.name"
        />
        <div class="info">
          <h3>{{ profile.name }}</h3>
          <h4 v-if="profile.status">{{ profile.status }}</h4>
          <p>
            <span v-html="profile.description"></span>
          </p>
        </div>
      </section>
    </div>
  </div>
</template>

<style scoped>
@import url('~/assets/css/profiles.css');

.collage .event {
  grid-template-columns: repeat(auto-fill, minmax(min(40%, 10.8rem), 1fr));
}

.collage .name {
  bottom: -1rem;
  background-color: var(--bg);
  color: var(--fg);
  border-radius: 2rem;
  border: 1px solid var(--primary);
}
</style>

<script setup>
import { ref } from "vue";

function resetLink() {
  setTimeout(() => {
    var newurl =
      window.location.protocol +
      "//" +
      window.location.host +
      window.location.pathname;
    window.history.pushState({ path: newurl }, "", newurl);
  }, 1);
}

const profiles = [
  {
    event: "Keynote Lecture",
    profiles: [
      {
        name: "Lorem Ipsum",
        status: "Guest of Honour",
        title: "",
        image: "Lorem Ipsum",
        description:
          "Lorem Ipsum.",
      },
      {
        name: "Lorem Ipsum",
        status: "Keynote Speaker",
        title:
          "Lorem Ipsum",
        image: "Lorem Ipsum",
        description:
          "Lorem Ipsum.",
      },
    ],
  },
  {
    event: "Guest Lectures",
    profiles: [
      {
        name: "Lorem Ipsum",
        image: "Lorem Ipsum",
        description: "Lorem Ipsum."
      },
    ]
  },
  {
    event: "Masterclasses",
    profiles: [
      {
        name: "Professor Ang Wee Han",
        image: "ang-wee-han",
        description:
          "Lorem Ipsum.",
      },
      {
        name: "Professor Chan Chun Yong, Eric",
        image: "chan-chun-yong-eric",
        description:
          "“Lorem Ipsum.",
      },
      {
        name: "A/Professor Hou Han Wei",
        image: "hou-han-wei",
        description:
          "Dr Han Wei Hou is an Associate Professor at the School of Mechanical and Aerospace Engineering (MAE), and Lee Kong Chian School of Medicine (LKCMedicine) at Nanyang Technological University Singapore (NTU). He is also an Adjunct Senior Research Scientist at Tan Tock Seng Hospital (TTSH), and currently serves as the Assistant Chair (Students) at MAE. Dr. Hou received his BEng (First Class Hons) and PhD degree in Biomedical Engineering at the National University of Singapore in 2008 and 2012, respectively. Upon graduation, he did his postdoctoral training at Massachusetts Institute of Technology (USA), and subsequently joined LKCMedicine as the inaugural LKCMedicine Postdoctoral Fellow in 2014. He started his research group at NTU (BioMicroSystems Laboratory, <a href='https://www.hwhoulab.com'>www.hwhoulab.com</a>) in 2018 and his research interests include microfluidics blood diagnostics, organ-on-chips, and cell-based biomanufacturing. He has authored over 60 peer-reviewed journal publications and filed 12 patents/patent applications. His recent research awards and accolades include World's Top 2% Scientists (By Stanford University) (2023), International Academy of Medical and Biological Engineering (IAMBE) Early Career Award (2022), NTU College of Engineering Research – Young Faculty Special Mention (2022), IFMBE Asia-Pacific Research Networking (APRN) Fellowship (2022) and International Society for Advancement of Cytometry (ISAC) Innovators (2021).",
      },
      {
        name: "Dr Lee Hwee Kuan",
        image: "lee-hwee-kuan",
        description:
          "Lorem Ipsum.",
      },
      {
        name: "Dr Li Jingmei",
        image: "li-jingmei",
        description:
          "Lorem Ipsum.",
      },
      {
        name: "A/Professor Wu Wei",
        image: "wu-wei",
        description:
          "Lorem Ipsum.",
      }
    ],
  },
];

const eventsOpen = ref(Array(profiles.length).fill(false));
</script>
