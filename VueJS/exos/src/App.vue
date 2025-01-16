<!-- Exo 1 -->
<!-- <template>
  <p>Compteur : {{ number }}</p>
  <button @click="updateNumber(1)">Incrémenter</button>
  <button @click="updateNumber(-1)">Décrémenter</button>
</template>

<script setup>
import { ref } from "vue";
const number = ref(0);

const updateNumber = (amount) => {
  number.value += amount;
};
</script>

<style scoped></style> -->

<!-- Exo 2 -->
<!-- <template>
  <input type="text" v-model="textInput" />
  <button @click="handleClick()" :class="`empty-${empty}`">Valider</button>
  <p>Valeur entrée : {{ textInput }}</p>
  <p>Compteur de clics : {{ counter }}</p>
</template>

<script setup>
import { ref } from "vue";

const counter = ref(0);
const empty = ref(true);
const textInput = ref("");

const updateNumber = (amount) => {
  counter.value += amount;
};

const updateColor = () => {
  if (textInput.value == "") {
    empty.value = true;
  } else {
    empty.value = false;
  }
};
const handleClick = () => {
  updateColor();
  updateNumber(1);
};
</script>

<style scoped>
.empty-true {
  background-color: red;
}
.empty-false {
  background-color: green;
}
</style> -->

<!-- Exo 3 -->
<!-- <template>
  <input type="text" placeholder="Nom d'utilisateur" v-model="loginInput" />
  <input type="password" placeholder="Mot de passe" v-model="passwordInput" />
  <br />
  <p v-if="password === ''">
    J'émets l'hypothèse, très cher utilisateur, que vous n'avez pas saisi votre
    mot de passe. Je vous saurais gré de faire preuve de bon sens.
  </p>
  <button v-else v-show="login !== ''">Connexion</button>
  <p v-if="LOGIN === loginPassword && PASSWORD === passwordInput">
    Bienvenue, {{ LOGIN }} !
  </p>
</template>

<script setup>
import { ref } from "vue";

const loginInput = ref("");
const passwordInput = ref("");

const LOGIN = "initialDeMonPrenomEtMonNomDeFamilleJeCrois";
const PASSWORD = "monNomMaDateDeNaissanceFacileARetenir";
</script>

<style scoped></style> -->

<!-- Exo 3 correction exercice -->
<!-- <template>
  <form @submit.prevent="onSubmit">
    <input type="text" placeholder="Nom d'utilisateur" v-model="loginInput" />
    <input type="password" placeholder="Mot de passe" v-model="passwordInput" />
    <br />

    <p v-if="passwordInput === ''">
      J'émets l'hypothèse, très cher utilisateur, que vous n'avez pas saisi
      votre mot de passe. Je vous saurais gré de faire preuve de bon sens.
    </p>

    <button v-else v-show="loginInput !== ''">Connexion</button>

    <p v-if="welcome">Bienvenue, {{ LOGIN }} !</p>
  </form>
</template>

<script setup>
import { ref } from "vue";

const loginInput = ref("");
const passwordInput = ref("");

const LOGIN = "initialDeMonPrenomEtMonNomDeFamilleJeCrois";
const PASSWORD = "monNomMaDateDeNaissanceFacileARetenir";

const welcome = ref(false);

function onSubmit() {
  if (loginInput.value === LOGIN && passwordInput.value === PASSWORD) {
    welcome.value = true;
  } else {
    welcome.value = false;
  }
}
</script>

<style scoped></style> -->

<!-- Exo 4-->
<!-- <template>
  <div>
    <div v-for="(article, index) in articles" :key="index">
      <h2>{{ article.title }}</h2>
      <div v-if="article.visible" v-html="article.content"></div>
      <button @click="article.visible = !article.visible">Masquer</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const articles = ref([
  {
    title: "Article 1",
    content: "<p>Contenu pour l'article 1.</p>",
    visible: true,
  },
  {
    title: "Article 2",
    content: "<p>Contenu pour l'article 2.</p>",
    visible: true,
  },
  {
    title: "Article 3",
    content: "<p>Contenu pour l'article 3.</p>",
    visible: true,
  },
]);
</script>

<style scoped></style> -->

<!-- Exo 5 -->
<!-- <template>
  <form @submit.prevent="onSubmit">
    <div>
      <input type="text" v-model="name" placeholder="Nom" />
    </div>
    <div>
      <input type="email" v-model="email" placeholder="Email" />
    </div>
    <div>
      <textarea v-model="comment" placeholder="Commentaire"></textarea>
    </div>
    <button :disabled="!allFieldsFilled">Valider</button>
  </form>

  <div v-if="submitted">
    <p>Nom : {{ name }}</p>
    <p>Email : {{ email }}</p>
    <p>Commentaire : {{ comment }}</p>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const name = ref("");
const email = ref("");
const comment = ref("");
const submitted = ref(false);

function onSubmit() {
  submitted.value = true;
}

const allFieldsFilled = computed(() => {
  return (
    name.value.trim() !== "" &&
    email.value.trim() !== "" &&
    comment.value.trim() !== ""
  );
});
</script>

<style scoped></style> -->

<!-- LA TODOLIST -->
<template>
  <div id="app">
    <h1>TodoList</h1>

    <div>
      <input type="text" v-model="newTask" placeholder="Nouvelle tâche" />
      <button :disabled="!newTask" @click="addTask">Ajouter</button>
    </div>

    <div>
      <input type="checkbox" v-model="hideCompleted" /> Masquer les tâches
      terminées
    </div>

    <div v-if="tasks.length === 0">
      <p>Aucune tâche à afficher.</p>
    </div>

    <ul>
      <li
        v-for="(task, index) in filteredTasks"
        :key="task.date"
        :class="{ completed: task.completed }"
      >
        <input type="checkbox" v-model="task.completed" />
        {{ task.title }}
      </li>
    </ul>
  </div>
</template>

<script setup>
import { ref, computed } from "vue";

const newTask = ref("");
const tasks = ref([]);
const hideCompleted = ref(false);

const addTask = () => {
  if (newTask.value.trim() !== "") {
    tasks.value.push({
      title: newTask.value,
      completed: false,
      date: Date.now(),
    });
    newTask.value = "";
  }
};

const filteredTasks = computed(() => {
  return tasks.value
    .filter((task) => !hideCompleted.value || !task.completed)
    .sort((a, b) => a.completed - b.completed);
});
</script>

<style>
.completed {
  text-decoration: line-through;
  color: grey;
}
</style>
