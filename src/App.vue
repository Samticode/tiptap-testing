<script>
import Editor from './components/Editor.vue'

export default {
  components: {
    Editor,
  },
}
</script>

<!-- -------------------------------------------------------------------------- -->

<template>

  <main>
    <section class="view-section"></section>
    <section class="editor-section">
      <Editor />
    </section>
  </main>

</template>

<!-- -------------------------------------------------------------------------- -->

<style scoped>
main {
  position: relative;
  height: 700px;
  max-width: 350px;
  border-radius: 2vmax;
  margin: 100px auto 0;
  background-color: #ffffffaa;
  overflow: hidden;

  .view-section {
    height: 60%;
    width: 100%;
    background-color: rgba(0, 0, 0, 0.544);
  }
  .editor-section {
    position: relative;
    height: 40%;
    width: 100%;

    display: flex;
    flex-direction: column;
    justify-content: space-between;
  }
}

</style>
