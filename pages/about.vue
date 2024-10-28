<template>
  <Masthead>
    <h1>About ISYF 2025</h1>
    <h3>
      About the event theme and goals!
    </h3>
  </Masthead>

  <main>
    <section>
      <h2>
        This Year's Theme:
        <PrimaryHighlight>
          Innovation Unified: Towards a Better Future
        </PrimaryHighlight>
      </h2>

      <p>
        "Innovation Unified" expresses the collaborative spirit and shared aspirations of young scientists in research and discovery of the world. This theme highlights the importance of unity and humility in the pursuit of groundbreaking discoveries and novel ideas. ISYF, likewise, facilitates meaningful conversations amongst bright young minds where diverse perspectives from delegates converge, exploring interdisciplinary approaches to solve global challenges. As young scientists, it is a common goal for us to envision a future of science and technology where collective innovation drives a positive change in society.
      </p>
    </section>

    <section class="colored goals">
      <h2>Our Goals</h2>

      <div class="goal red">
        <div>
          <h3>Inspire Passion for Science Among Youth</h3>
          <p>
            ISYF aims to provide students who are highly inquisitive and
            passionate about the sciences with ample opportunities to share and
            discuss their interest in Science, technology and scientific
            research. They will be exposed to many fields of science which will
            broaden their outlook and understanding of the scientific world.
            Invited Nobel laureates and eminent scientists will inspire them
            through stories of their own life experiences and scientific
            discoveries. These interactions will help create greater awareness
            among the youth about the importance of broad-based knowledge, fuel
            their curiosity, engender relentless tenacity and a global outlook
            when considering the pursuit of science as a meaningful and
            fulfilling endeavour.
          </p>
        </div>
      </div>

      <div class="goal green">
        <div>
          <h3>
            Establish Cooperation and Friendship Amongst Young Talented Science
            Students
          </h3>
          <p>
            Students will have many opportunities to interact in different
            cross-cultural groups and forge strong bonds with each other
            throughout the Forum. Activities are designed to promote mutual
            cooperation, understanding and appreciation of each other’s diverse
            cultures while sharing a common passion in science, technology and
            research.
          </p>
        </div>
      </div>

      <div class="goal purple">
        <div>
          <h3>Build Capacities of Science Educators</h3>
          <p>
            Through professional sharing and discussions among Science
            educators, ISYF helps build the competencies of teachers who are
            navigating an evolving educational landscape.
          </p>
        </div>
      </div>
    </section>
  </main>
</template>

<style>
.masthead::before {
  color: var(--bg);
  background-image: url("/images/aboutbg2.webp");
  filter: brightness(40%);
  background-size: cover;
  background-repeat: no-repeat;
  background-position: 43% 50%;
}
section.goals {
  border: 1px solid black;
  border-radius: 16px;
  padding: 0;
  overflow: hidden;
  margin-inline: -0.75rem;
}
.goals > * {
  padding-inline: 1rem;
}
.goals > * + * {
  border-top: 1px solid black;
}
.goals h2 {
  margin: 0;
  padding-block: 0.5rem;
}
.goal {
  display: grid;
  grid-template-columns: 1rem 1fr;
  padding-left: 0;
}
.goal::before {
  content: "";
  display: inline-block;
  background-color: purple;
  border-right: 1px solid var(--fg);
}
.goal > * {
  padding-left: 1rem;
}

.red::before {
  background-color: var(--red);
}
.green::before {
  background-color: var(--green);
}
.purple::before {
  background-color: var(--purple);
}
</style>

<style scoped>
.collapsible {
  background-color: #eee;
  color: #444;
  cursor: pointer;
  padding: 18px;
  width: 100%;
  border: none;
  text-align: left;
  outline: none;
  font-size: 15px;
}

.active,
.collapsible:hover {
  background-color: #ccc;
}

.content {
  padding: 0 18px;
  display: none;
  overflow: hidden;
  background-color: #f1f1f1;
}
</style>

<script setup>
import PrimaryHighlight from "../components/primaryHighlight.vue";
import { ref, watch, onMounted, onUnmounted } from "vue";
definePageMeta({
  layout: "masthead",
});

onMounted(() => {
  var coll = document.getElementsByClassName("collapsible");
  var i;
  for (i = 0; i < coll.length; i++) {
    coll[i].addEventListener("click", function () {
      this.classList.toggle("active");
      var content = this.nextElementSibling;
      if (content.style.display === "block") {
        content.style.display = "none";
      } else {
        content.style.display = "block";
      }
    });
  }
});
</script>
