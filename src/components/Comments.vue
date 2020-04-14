
<template>      
      <div class="container">
      <h1>Comentarios</h1>
      <hr />
  
    <div class="form-todo form-group">
      <p>
        <input placeholder="autor" name="message" 
        class="form-control" v-model="name">
      </p>
      <p>
      <textarea placeholder="Comentatio" name="message"
      class="form-control" v-model="message"></textarea>
    </p>
    <button type="submit" class="btn btn-primary" v-on:click="adicionar">Comentar</button>
    </div>
  
  <div class="list-group">
      <div class="list-group-item" v-for="(comment, index) in allComments">
        <span class="comment_author">Autor: <strong>{{ comment.name }}</strong></span>
       
        <p> Menssagem: {{ comment.message }}</p>
       
       <div>
        <a href="#" v-on:click.prevent="removeComment(index)" title="Excluir">Excluir Menssagem</a> 
       </div>
      </div>
  </div>
  <hr />
</div>    
</template>

<script>
export default{

    data(){
     return{
      comments:[],
      name:'',
      message:''
     }
   },
   methods:{
        adicionar(){
          if(this.message.trim() === ''){
            return;
          }
          this.comments.push({
            name:this.name,
            message: this.message
          });
          this.name='',
          this.message=''
        },
        removeComment(index){
          this.comments.splice(index,1)
        }
        
       },
       computed:{
          allComments(){
            return this.comments.map(comment =>({
              ...comment,
              name: comment.name.trim() === ' ' ? 'Anônimo' : comment.name
            }))
          }
        }
  
  }   
</script>
