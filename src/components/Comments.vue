<template>
    <div class="container mt-5">
    <h3>Application in Vue.js</h3>
    <hr />
    <div class="mb-3">
        <label for="name" class="form-label">Name</label>
        <input v-model="name" type="text" class="form-control" id="name" aria-describedby="emailHelp">
    </div>
    <div class="mb-3">
        <label for="message" class="form-label">Message</label>
        <textarea v-model="message" type="text" class="form-control" id="message"></textarea>
    </div>
    <button v-on:click="addComment"  class="btn btn-primary mb-5">Comment</button>
    <h3>Comments</h3>
    <hr /> 

    <div v-for="(comment, index) in allComments" v-bind:key="comment.id" class="card mb-3" >
        <div  class="card-body">
            <h5 class="card-title"><strong>{{ comment.name }}</strong></h5>
            <hr/>
            <p class="card-text text-muted">{{ comment.message }}</p>
            <a href="#" v-on:click=removeComment(index) class="card-link text-danger"><i class="far fa-trash-alt"></i> Excluir</a>
        </div>
</div>
</div>
</template>

<script>
export default {
  data() {
      return{
        comments: [],
        name: "",
        message: "",
  }

  },
  methods: {
    addComment() {
      if (this.message == "") return;
      this.comments.push({
        name: this.name,
        message: this.message,
      });
      this.name = "";
      this.message = "";
    },
    removeComment(index) {
      console.log(index);
      this.comments.splice(index, 1);
    },
  },
  computed: {
      allComments(){
          return this.comments.map(comment => ({
              ...comment,
              name: comment.name.trim() == '' ? 'Anonymous' : comment.name
          }))
      }
  },
  watch:{}
};
</script>
