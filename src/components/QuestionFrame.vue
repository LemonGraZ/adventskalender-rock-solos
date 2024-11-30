<template>
  <v-container
    class="fill-height fill-width align-center flex-column pt-10 ga-5"
    style="max-width: 800px"
  >
    <div class="max-auto circle elevation-6">
      {{ day }}
    </div>
    <span class="text-h4 question text-center">Woher stammt dieses Solo?</span>
    <span class="question text-center">Jeweils 1 Punkt für Band, Song und Gitarrist.</span>
    <audio
      class="mx-auto w-100 rounded-lg"
      controls
      :src="audioPath"
      type="audio/mpeg"
    >
      Ein Problem
    </audio>
    <v-btn variant="tonal">
      Hier gibts' die Lösung
      <v-dialog v-model="showSolution" activator="parent" max-width="800px" eager>
        <v-card class="rounded-lg pa-5 ga-5" width="auto" title="Na, richtig geraten?">
          <iframe
            style="border-radius: 12px"
            :src="answer['embed']+'&theme=1'"
            width="100%"
            height="152"
            frameBorder="0"
            allowfullscreen=""
            allow="clipboard-write; encrypted-media; fullscreen; picture-in-picture"
          ></iframe>
          <v-card class="pa-4 rounded-lg" variant="tonal">
            Gitarrist:
            <span style="font-weight: 500">{{ answer["guitarist"] }}</span>
          </v-card>
          <v-card-actions>
            <v-btn block @click="showSolution = false">Schließen</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-btn>
  </v-container>
</template>

<script>
import answersJSON from "@/assets/answers.json";

export default {
  props: {
    day: Number,
  },
  data: () => ({
    showSolution: false,
  }),
  computed: {
    audioPath() {
      return `${window.location.origin}/adventskalender-rock-solos/${this.day}.m4a`;
    },
    answer() {
      return answersJSON[this.day - 1];
    },
  },
};
</script>

<style>
.circle {
  width: 50vw;
  max-width: 200px;
  height: 50vw;
  max-height: 200px;
  background-color: #c4b180;
  border-radius: 50%;
  color: #063125;
  font-size: min(25vw, 100px);
  text-align: center;
  vertical-align: middle;
  line-height: min(50vw, 200px);
}

.question {
  color: #c4b180;
}
</style>
