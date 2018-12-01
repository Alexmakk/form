<template>
<div class="formInput">
    <form 
    v-if = "!showTable"
    v-on:submit.prevent = "showTable = true">
        <div class='form-group'>
            <label>Email</label>
            <input type="text" class='form-control' name='email'
                v-model="email">
        </div>
        <div class='form-group'>
            <label>First name</label>
            <input type="text" class='form-control' name='firstname'
                v-model="firstName">
        </div>
        <div class='form-group'>
            <label>Last name</label>
            <input type="text" class='form-control' name='lastname'
                v-model="lastName">
        </div>
        <div class='form-group'>
            <label>Phone</label>
            <input type="text" class='form-control' name='phone'
                v-model="phone">
        </div>
        <div>
            <label>Guests</label>
            <input type = "button"
            class="btn btn-primary"
            value = "+"
            v-on:click= "addGuest">
        </div>
        <div class='form-group' 
            v-for = "(guest, key, index) in guests" 
            v-bind:key = "key">
            <label v-on:dblclick = "deleteGuest(key)">
                Guest {{ index + 1 }}
            </label>
            <input type="text" class='form-control'
                v-model= "guests[key]"
            >
        </div>
        <hr>
        <input type="submit" value='Send Data' class='btn btn-success'>
    </form>
    <div v-else>
        <label>All done!</label>
        <table class="table table-bordered">
            <tr>
                <td>Email</td>
                <td>{{ email }}</td>
            </tr>
            <tr>
                <td>Name</td>
                <td>{{ fullName }}</td>
            </tr>
            <tr>
                <td>Phone</td>
                <td>{{ phone }}</td>
            </tr>
            <tr>
                <td>Guests</td>
                <td>
                    <ul class="list-group">
                        <li class="list-group-item" 
                            v-for = "(guest, key, index) in guests">
                            Guest {{ index + 1 + ':' +' '+ guest }}
                        </li>
                    </ul>
                </td>
            </tr>
        </table>
    </div>
</div>


</template>               

<script>

export default {
  data() {
     return {
        email: '',
        firstName: '',
        lastName: '',
        phone: '',
        guests: {},
        guestIterator: 0,
        showTable: false
    }
  },
  computed: {
      fullName() {
          return this.firstName + ' ' + this.lastName;
      }
  },
  methods: {
      addGuest() {
          this.guestIterator++;
          this.$set(this.guests, this.guestIterator, '');
      },
      deleteGuest(key) {
          //console.log(key);
          this.$delete(this.guests, key);
      }
  }
}
  
</script>

<style scoped> 
.formInput{
    margin: 0 auto;
    width: 40%;
}


</style>
