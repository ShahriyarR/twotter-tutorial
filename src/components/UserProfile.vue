<template>
  <div class="user-profile">
    <div class="user-profile__sidebar">
      <div class="user-profile__user-panel">
          <h1 class="user-profile__username">@{{ user.username }}</h1>
          <div class="user-profile__admin-badge" v-if="user.isAdmin">
              Admin
          </div>
          <div class="user-profile__follower-count">
            <strong>Followers: </strong> {{ followers }}
          </div>
      </div>
      <CreateTwootPanel @add-twoot="addTwoot"/>
    </div>
    <div class="user-profile__twoots-wrapper">
          <TwootItem 
                    v-for="twoot in user.twoots" 
                    :key="twoot.id" 
                    :username="user.username" 
                    :twoot="twoot" 
          />
    </div>  
  </div>
</template>

<script>
import TwootItem from "./TwootItem";
import CreateTwootPanel from "./CreateTwootPanel";

export default {
  name: 'UserProfile',
  components: { CreateTwootPanel, TwootItem },
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: '_MitchellRomney',
        firstName: 'Mitchell',
        lastName: 'Romney',
        email: 'mitchellromney@theearthissquare.com',
        isAdmin: false,
        twoots: [
            {id: 1, content: 'Twootter is Amazing!'},
            {id: 2, content: 'Dont forget to subscribe.'}
        ]
      }
    }
  },

  methods: {
    addTwoot(twoot) {
      this.user.twoots.unshift({id: this.user.twoots.length + 1, content: twoot})
    }
  }
};
</script>

<style lang="scss" scoped>
.user-profile {
    display: grid;
    grid-template-columns: 1fr 3fr;
    grid-gap: 50%;
    padding: 50px 5%;

    .user-profile__user-panel {
      display: flex;
      flex-direction: column;
      padding: 20px;
      background-color: white;
      border-radius: 5px;
      border: 1px solid #DFE3E8;
      margin-bottom: auto;

         h1 {
           margin: 0;
        } 

        .user-profile__admin-badge {
          background: rebeccapurple;
          color: white;
          border-radius: 5px;
          margin-right: auto;
          padding: 0 10px;
          font-weight: bold;
      }
    }
  
  .user-profile__twoots-wrapper {
    display: grid;
    grid-gap: 10px;
    margin-bottom: auto;
  }
}

</style>
