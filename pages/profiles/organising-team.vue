<template>
  <h1>The Organising Team</h1>

  <div class="comm" v-for="comm in profiles">
    <div class="comm-title">{{ comm.name }}</div>
    <div class="comm-showcase">
      <img
        class="comm-img"
        :src="'/images/profiles/organising-team/' + comm.image + '.webp'"
      />
      <div class="comm-description">
        <p v-html="comm.description" class="commDescription"></p>
        <p v-html="comm.imgCaption"></p>
      </div>
    </div>
  </div>
</template>

<style scoped>

.commDescription {
  margin-top: 0rem;
}
.comm {
  margin-block: 3rem 3.5rem;
}

.comm-title {
  font-size: 56px;
  font-weight: bold;
  margin-block: 0 -0.25rem;
  margin-left: 0.5rem;
  line-height: 0.9em;
  margin-bottom: 1rem;

  color: var(--primary);
}

.comm-showcase {
  display: grid;
  grid-template-columns: 6fr 4fr;
  gap: 2rem;
}

.comm-img {
  width: 100%;
  border-radius: 4px;
}

@media screen and (max-width: 900px) {
  .comm-title {
    font-size: 48px;
  }

  .comm-showcase {
    grid-template-columns: 1fr;
    gap: 0.5rem;
  }

  .comm-description {
    margin-top: 0;
  }

  .comm-showcase p {
    margin-block: 0.75rem;
  }
}
@media screen and (max-width: 600px) {
  .comm-title {
    font-size: 38px;
    margin-bottom: -0.075em;
  }
}
</style>

<script setup>
const profiles = [
  {
    name: 'Admin & Operations',
    image: 'ano',
    description:
      'The Admin & Operations team are dedicated individuals who work tirelessly to ensure your ISYF experience is smooth and seamless. They orchestrate and tie events together behind the scenes to bring you a truly fulfilling experience!',
    imgCaption:
      '<b>LEFT TO RIGHT:</b> Tan Myn Jae, Hsiao Li Chia, Heah Xin Ler, Leung Hoi Yan, Nyeo Zheng Xin Andre, Lau Ray Kai Elliot',
  },
  {
    name: 'Ceremonies',
    image: 'ceremonies',
    description:
      'The Ceremonies team have planned two major events for ISYF: The ISYF Keynote Lecture and Closing Lunch. <br/><br/> The Keynote Lecture is a great chance for you to hear more from Nobel laureates and eminent scientists on issues surrounding the theme of the forum. You also get a chance to pose your very own questions to the experts in a forum styled question-and-answer session. <br/><br/> The Closing Ceremony on the other hand is our way of ending off ISYF on a high note, so be ready with your cameras to take some memorable photos!',
    imgCaption:
      '<b>LEFT TO RIGHT:</b> Chong Shao Yi Asher, Poh Zi Qian Anderson, Ang Shi Qi Georia, Woo Yu Rou Elena, Jacinda Kung Jiexin, Seah Yuheng, Ryan Quek Kai En',
  },
  {
    name: 'Masterclasses',
    image: 'dnm',
    description:
      'The Masterclasses team seek to connect you to knowledgeable and prominent scientists, allowing you to explore new perspectives and gain new insights on notable scientific research. We hope you stay curious and embrace this valuable oportunity with eminent scientists and Nobel laureates!',
    imgCaption:
      '<b>1ST ROW:</b> Koh Yee Ting, Chen Zimo, Tasha Rahardja, Eunice Lim Yu Xin <br/><b>2ND ROW:</b> Ray Lee Jun Rui, Gideon Tan Kah Yong, Dallas Win, Wipasstharitsakul Possaweekrish',
  },
  {
    name: 'Media & Publications',
    image: 'mnp',
    description:
      'The Media & Publications team constantly strive to deliver to you the best publicity efforts and media projects. Stay informed with the ISYF website, Instagram pages and the student handbook. Also enjoy the unique designs on the ISYF merchandise made by our very own designers. We hope that the content we create will be able to add to your ISYF experience!',
    imgCaption:
      '<b>1ST ROW:</b> Poon Yee way <br/><b>2ND ROW:</b> Loo Xin En Nicole, Zhu Zixuan <br/><b>3RD ROW:</b> Yap Leia, Chan Li Xuan Rianne, Quek Zhi Xing <br/><b>4TH ROW:</b> Wu Cheng Sheng, Alvin Liu En Yu, Ni Haoran, Lin Tai Lai <br/><b>External Sub-comm:</b> Alvin Liu En Yu, Lin Tai Lai, Wu Cheng Sheng, Yap Leia',
  },
  {
    name: 'Recreational Activities',
    image: 'reacts',
    description:
      'The Recreational Activities team are in charge of ensuring you enjoy yourself thoroughly, through fun activities like the Singapore Discovery Tour, Cultural Hour and Exhibitions. ISYF is the perfect avenue to meet new friends who are passionate in science, and we hope that these activities provide a great time for you to bond with them!',
    imgCaption:
      '<b>1ST ROW:</b> Hu Mei, Ng Zhi Xuan, Jess Pee Xue Qi, Lim Ci Rui <br/> <b>2ND ROW:</b> Chen Tingyu, Niu Hongrui, Liu Zhile, Ma Yicheng Ethan, Tan Yi Wei ',
  },
  {
    name: 'Science Activities',
    image: 'sciacts',
    description:
      'The Science Activities team will enrich your learning with various activities to dive deeper into the world of Science. Do look forward to science excursions and challenges, which will be sure to provide something new for everyone!',
    imgCaption:
      '<b>1ST ROW:</b> Fong Yi Han Janelle, Chng Yun Jing Crystal, Lim Jing En, Huang Ziyan, Eugene Lee Yu Feng <br/> <b>2ND ROW:</b> Ng Xin Yi, Aydan Oh Yi Qi, Ong Kai Xiang, Xu Kangyou ',
  },
];
</script>
