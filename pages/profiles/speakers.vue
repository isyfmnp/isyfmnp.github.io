<template>
  <h1>Invited Speakers</h1>

  <p>
    Click on each speakers name to see their profile! You can also scroll down and see
    further details
  </p>

  <div class="collage">
    <section class="event" v-for="(event, eventIndex) in profiles" :class="{ 'event-open': eventsOpen[eventIndex] }">
      <h3 class="event-title">{{ event.event }}</h3>
      <a class="profile" v-for="profile in event.profiles" :href="'#' + profile.name.replaceAll(' ', '')"
        @click="resetLink">
        <img class="profile-img" :src="'/images/profiles/speakers/' + profile.image + '_square.webp'" alt="" />
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
        <img :src="'/images/profiles/speakers/' + profile.image + '.webp'" :alt="profile.name" />
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
        name: "Professor Lim Keng Hui",
        status: "Guest of Honour",
        image: "lim-keng-hui",
        description:
          "Placeholder text. Profile to be completed together with image.",
      },
      {
        name: "Professor Hartmut Michel",
        status: "Keynote Speaker",
        image: "hartmut-michel",
        description:
          "Professor Hartmut Michel is a German biochemist who was awarded the 1988 Nobel Prize in Chemistry “for the determination of the three-dimensional structure of a photosynthetic reaction centre”. Photosynthesis is considered to be “the most important chemical reaction on earth”. He shared the prize with Johann Deisenhofer and Robert Huber. Professor Michel studied biochemistry in Tübingen and Munich. He got his Ph.D. from the University of Würzburg in 1977 for work in bioenergetics. In 1979 he moved to the Max Planck Institute of Biochemistry at Martinsried near Munich with his supervisor Dieter Oesterhelt. There he intensified his work on the crystallisation of membrane proteins which was considered to be impossible. Because of his success he became director at the Max Planck Institute of Biophysics in Frankfurt am Main, Germany, in 1987, where he still works. Professor Michel expanded his work onto other important membrane proteins, often of medical importance. Most successful he has been with secondary active transporters. This kind of membrane-integrated proteins enable and drive the specific transport of substances like nutrients and building blocks across biological membranes, and with terminal oxidases. These latter enzymes use electrons provided e.g. by cytochrome c or ubiquinol to reduce oxygen to water and use the vast amount of energy inherent in this reaction for powering life. Professor Michel is a member or foreign member of many learned societies: among others Leopoldina (German National Academy of Science), the Chinese Academy of Sciences, the National Academy of Sciences (U.S.) and the Royal Society London. He is an outspoken critic of producing and using biofuels, arguing that it is an inefficient and detrimental use of agricultural land, which he believes is better allocated to producing food to feed the increasing human population on earth.",
      }
    ],
  },
  {
    event: "Guest Lectures",
    profiles: [
      {
        name: "Professor Sow Chorng Haur",
        image: "sow-chorng-haur",
        description: "Professor Sow Chorng Haur received his Bachelor of Science Degree (1st Class) in Physics from the National University of Singapore (NUS) in 1991. He received his Master of Science degree in Physics after spending two more years in NUS for research. Professor Sow then completed his PhD degree in the University of Chicago in 1998. For the next two years, he worked as a postdoctoral fellow at Bell Laboratory, Lucent Technologies. He then returned and joined the Department of Physics, NUS in 2001. He is now the Vice Dean (Outreach and Admissions) of the Faculty of Science and the Vice President of the Singapore National Academy of Science. \n\nProfessor Sow’s research interests include carbon nanotubes, nanomaterials and the fundamental studies of 2D materials (e.g. graphene, dichalcogenide and phosphorene) and their applications. He has worked on developing a laser pruning method to create unique 2D and 3D structures made of carbon nanotubes, the synthesis of a wide variety of nanoscale metallic oxide materials and the assembly of nanowires and nanowalls. Professor Sow, with over 270 publications, has authored and co-authored many papers in the field of nanoscience and nanomaterials. \n\nProfessor Sow is also known for being an inspiring educator, having been awarded various teaching awards such as the University Award: Outstanding Educator Award from NUS in 2008, and the Faculty Teaching Excellence Award from 2002 to 2013."
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
          "Professor Ang Wee Han is a Professor of Inorganic Chemistry at the National University of Singapore (NUS). An alumni of the Chinese High School and Hwa Chong Junior College, he graduated from Imperial College London in 1995 with BSc (Hons) First Class under the Singapore Armed Forces Merit Scholarship. He went on to serve in the Republic of Singapore Navy as a Naval Combat Officer and was honourably discharged in 2003 after 8 years of service. He chose to return to academia to pursue his PhD studies at Ecole Polytechnique Federal de Lausanne, Switzerland till 2007 followed by a postdoctoral research stint at the Massachusetts Institute of Technology. He joined NUS in 2009 to embark on his independent academic career and has been there since. <br><br>Professor Ang’s current research lies at the intersection of inorganic chemistry and biology, and he is actively investigating new metal-containing compounds for use in cancer therapy and as targeted antibiotics. He is also passionate about the study of trace metals and their roles in flavour science, having co-founded a start-up company developing alternative protein products with meat-like flavours. Professor Ang is currently holding concurrent management appointments as an Associate Provost and Vice-Deans at NUS. He is also the Chairperson of the Advisory Committee on Hazardous Substances and Toxic Waste under the National Environmental Agency and represents Asia on the Executive Committee of the Society of Biological Inorganic Chemistry.",
      },
      {
        name: "Professor Chan Chun Yong, Eric",
        image: "chan-chun-yong-eric",
        description:
          "Professor Eric Chan is a pharmaceutical scientist and pharmacist in the Department of Pharmacy and Pharmaceutical Sciences, National University of Singapore (NUS). His research interests are (1) physiologically-based pharmacokinetic-pharmacodynamic (PBPK-PD) modeling of pharmacology and toxicology, (2) xenobiotic-derived reactive metabolite research with specific focus on interaction with biological proteins and (3) metabolism-driven systems biology modeling of pathology, pharmacology, toxicology and mammalian host-bacteria interactions. <br><br>Professor Chan is currently Deputy Head (Research) and a member of the Faculty Promotion and Tenure Committee (FPTC). He is the Executive Editor of the British Journal of Clinical Pharmacology. He is also an editorial advisory board member of the Biochemical Pharmacology, Drug Metabolism and Disposition and Journal of Chromatography B. He is an expert consultant at the Hyloris Pharmaceuticals and the Agency for Science, Technology and Research (A*STAR) Experimental Drug Development Centre (EDDC), and a member of the Singapore Food Agency (SFA) Novel Food Safety Expert Working Group. <br><br>Professor Chan was awarded the Dean’s Chair Professorship in the Faculty of Science (2015-2018). He was six times a recipient of the Faculty of Science Teaching Excellence Award and four times the NUS Annual Teaching Excellence Award. He also received the Faculty of Science Young Scientist Award (2010) and Outstanding Scientist Award (2014).",
      },
      {
        name: "A/Professor Hou Han Wei",
        image: "hou-han-wei",
        description:
          "Professor Han Wei Hou is an Associate Professor at the School of Mechanical and Aerospace Engineering (MAE), and Lee Kong Chian School of Medicine (LKCMedicine) at Nanyang Technological University Singapore (NTU). He is also an Adjunct Senior Research Scientist at Tan Tock Seng Hospital (TTSH), and currently serves as the Assistant Chair (Students) at MAE. Professor Hou received his BEng (First Class Hons) and PhD degree in Biomedical Engineering at the National University of Singapore in 2008 and 2012, respectively. Upon graduation, he did his postdoctoral training at Massachusetts Institute of Technology (USA), and subsequently joined LKCMedicine as the inaugural LKCMedicine Postdoctoral Fellow in 2014. He started his research group at NTU (BioMicroSystems Laboratory, <a href='https://www.hwhoulab.com'>www.hwhoulab.com</a>) in 2018 and his research interests include microfluidics blood diagnostics, organ-on-chips, and cell-based biomanufacturing. He has authored over 60 peer-reviewed journal publications and filed 12 patents/patent applications. His recent research awards and accolades include World's Top 2% Scientists (By Stanford University) (2023), International Academy of Medical and Biological Engineering (IAMBE) Early Career Award (2022), NTU College of Engineering Research – Young Faculty Special Mention (2022), IFMBE Asia-Pacific Research Networking (APRN) Fellowship (2022) and International Society for Advancement of Cytometry (ISAC) Innovators (2021).",
      },
      {
        name: "Dr Lee Hwee Kuan",
        image: "lee-hwee-kuan",
        description:
          "Dr Lee Hwee Kuan earned his Ph.D. from Carnegie Mellon University in Pittsburgh, PA, USA, in theoretical physics. Currently, he serves as the Head of the Imaging Informatics Division as well as the Deputy Director for Training and Talent development at the Bioinformatics Institute, A*STAR in Singapore. Dr Lee's expertise lies in the development and deployment of machine learning and deep learning algorithms. With a strong foundation in theoretical physics, Dr Lee brings a unique perspective to the field of artificial intelligence, driving innovative solutions for both clinical and biological applications. \n\n At present, Dr Lee leads a laboratory dedicated to the advancement of Artificial Intelligence (AI) research for clinical and biological purposes. His research endeavours encompass a broad spectrum of activities, from fundamental AI-centric investigations to practical AI applications. Dr Lee's work is particularly influenced by high-impact clinical use cases, driving theoretical AI development. His laboratory addresses critical areas such as diagnostics in cancers, cardiology, dermatology, and interventional radiology. In the realm of biology, Dr Lee's team develops bioinformatics pipelines for spatial omics and single-cell analysis, alongside pioneering AI applications in protein science and drug discovery. Beyond his role at the Bioinformatics Institute, Dr Lee holds significant appointments in various local universities and research institutions.",
      },
      {
        name: "Dr Li Jingmei",
        image: "li-jingmei",
        description:
          "Dr Li Jingmei is a Principal Scientist at the Genome Institute of Singapore, A*STAR. She obtained her PhD in Medical Science from Karolinska Institutet, Stockholm, Sweden, in 2011. <br><br>In 2014, Dr Li was among fifteen young women scientists globally who were awarded the UNESCO-L'Oréal International Fellowships. She returned to Singapore in 2017 under the aegis of a National Research Foundation Fellowship, an award that supports early career researchers up to S$3 million in funding over five years. For her work on mammographic density and its impact on women’s health, Li received the 2017 Young Scientist Award at the President’s Science and Technology Awards. Dr Li is also a national finalist representing Singapore in the mid-career scientist category in the 2022 Underwriters Laboratories - ASEAN-U.S Science Prize for Women - Artificial Intelligence (AI) in Health and Safety. In 2024, she was recognized as an A*STAR Fellow. <br><br>A woman in science doing science for women, Dr Li's research endeavors to improve lives through disease risk prediction. Her scientific findings are currently being applied in a pilot risk-based breast cancer screening study in Singapore.",
      },
      {
        name: "Professor Takaaki Kajita",
        image: "takaaki-kajita",
        description:
          "Professor Takaaki Kajita is the Special University Professor at The University of Tokyo, and also the Director of the Institute for Cosmic Ray Research (ICRR) of The University of Tokyo. Professor Kajita received his Ph.D. from The University of Tokyo School of Science in 1986, and has been researching Kamiokande and Super-Kamiokande detectors at the Kamioka Observatory in central Japan. In 1998, at the Neutrino International Conference held in Takayama, Gifu, he showed the analysis results which provided strong evidence for atmospheric neutrino oscillations. In 2015 he shared the Nobel Prize in Physics for his role in discovering atmospheric neutrino oscillations. Currently, he is the project leader for the KAGRA Project, aiming to explore gravitational wave astronomy."
      },
      {
        name: "Sir Tim Hunt",
        image: "tim-hunt",
        description:
          "Sir Tim Hunt grew up in Oxford, where he became fascinated by science at the Dragon School. At 14, he entered Magdalen College School, where his interest in biology grew. Sir Hunt entered Clare College, Cambridge in 1961 to read Natural Sciences. He joined the Department of Biochemistry in 1964 as a graduate student working on the control of haemoglobin synthesis. In 1968 he moved to the Albert Einstein College of Medicine in New York as a postdoctoral Fellow with Irving London. <br><br>Sir Hunt returned to the Department of Biochemistry in Cambridge in 1971 where he continued to work on translational control throughout the 1970s. He taught summer courses at the Marine Biological Laboratory, Woods Hole, Massachusetts from 1977 to 1983, looking at changes in protein synthesis in sea urchin and clam eggs after fertilisation. In 1979, he helped Joan Ruderman and Eric Rosenthal with experiments on the translational control of maternal mRNA in clam eggs, where two of the major mRNAs concerned later turned out to be the A and B-type cyclins. By 1982, Sir Hunt had almost exhausted the potential of sea urchin eggs, but it was then that he performed the experiment that led to the discovery of cyclins and subsequent research on the control of the cell cycle. In 1990, Sir Hunt joined ICRF (now The Francis Crick Institute) in London. He became a fellow of the Royal Society in 1991, a foreign associate of the US National Academy of Sciences in 1999 and shared the Nobel Prize for Physiology or Medicine with Lee Hartwell and Paul Nurse in 2001. He enjoys cooking, photography and making up problems for Molecular Biology of the Cell with his friend John Wilson. In 2016, he and his wife Mary Collins moved to Okinawa, where Mary was the Provost of OIST (Okinawa Institute of Science and Technology). In 2022, Mary was appointed Director of the Blizard Institute of QMUL and they returned to London."
      },
      {
        name: "A/Professor Wu Wei",
        image: "wu-wei",
        description:
          "Professor Wu Wei received his PhD degree at Swiss Federal Institute of Technology in Lausanne (EPFL), Switzerland. Prior to joining NTU, he was a Postdoctoral Scholar at Stanford University, USA. He is currently an Associate Professor at Nanyang Technological University (NTU), Singapore, and serves as the President of Society for Rock Mechanics & Engineering Geology (SRMEG), the Associate Editor for International Journal of Rock Mechanics and Mining Sciences, and the Assistant Chair for Research in School of Civil and Environmental Engineering (CEE) at NTU. Professor Wu’s research focuses on experimental geophysics and energy geomechanics, with emphasis on underground space development, geo-energy extraction and storage, as well as induced geohazards due to climate change and energy extraction. He currently leads several research projects on geothermal energy exploration, underground energy storage, and urban geophysical survey in Singapore. He has received numerous awards, such as NTU CEE Research Award in 2023, SRMEG Outstanding Paper Award in 2017, and Swiss Perspective Researcher Fellowship in 2013.",
      },
      {
        name: "Professor Yael Tauman Kalai",
        image: "yael-tauman-kalai",
        description:
          "Professor Yael Tauman Kalai is an Ellen Swallow Richards Professor at the Massachusetts Institute of Technology (MIT). Professor Kalai earned a BSc in Mathematics from the Hebrew University of Jerusalem, an MS in Computer Science and Applied Mathematics from The Weizmann Institute of Science, and a PhD in Computer Science from the Massachusetts Institute of Technology. Professor Kalai's honors include an Outstanding Master's Thesis Prize (Weizmann Institute of Science, 2001), and the George M. Sprowls Award for Best Doctoral Thesis in Computer Science (MIT, 2007). She is the recipient of the 2022 ACM Prize in Computing and is a Fellow of the International Association for Cryptologic Research (IACR). Additionally, Professor Kalai was an invited speaker at the International Congress of Mathematics (ICM, 2018)."
      }
    ],
  },
];

const eventsOpen = ref(Array(profiles.length).fill(false));
</script>
