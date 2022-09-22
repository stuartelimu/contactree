<script>
  export default {
    data() {
      return {
        contact: '',
        editedContact: null,
        statuses: ['available','unavailable'],
        contacts: [
          {
            tel: '0702324377',
            status: 'available'
          },
          {
            tel: '0702324317',
            status: 'unavailable'
          }
        ]
      }
    },

    methods: {
      submitContact() {
        if (this.contact.length === 0) return;

        if (this.editedContact === null ) {
          this.contacts.push({
            tel: this.contact,
            status: 'available'
          })
        } else {
          this.contacts[this.editedContact].tel = this.contact;
          this.editedContact =null;
        }

        this.contact = ''
      },

      deleteContact(index) {
        this.contacts.splice(index,1)
      },

      editContact(index) {
        this.contact = this.contacts[index].tel;
        this.editedContact = index;

      },

      changeStatus(index) {
        let currentIndex = this.statuses.indexOf(this.contacts[index].status)
        if(++currentIndex > 1) currentIndex = 0;
        this.contacts[index].status = this.statuses[currentIndex]
      }
    }
  }

</script>

<template>
  <div class="container">
    <div class="text-center mt-5">Contactree</div>

    <!-- inputs -->
    <div class="d-flex mt-3">
      <input v-model="contact" type="text" placeholder="Enter Telephone" class="form-control">
      <button @click="submitContact" class="btn btn-warning rounded-0">SUBMIT</button>
    </div>

    <!-- table -->
    <table class="table table-bordered mt-3">
      <thead>
        <tr>
          <th scope="col">Number</th>
          <th scope="col">Status</th>
          <th scope="col" class="text-center">#</th>
          <th scope="col" class="text-center">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(contact, index) in contacts" :key="index">
          <td>{{ contact.tel }}</td>
          <td style="width: 200px"><span class="pointer" @click="changeStatus(index)">{{ contact.status }}</span></td>
          <td>
            <div @click="editContact(index)" class="text-center pointer"><span class="fa fa-pen text-success"></span></div>
          </td>
          <td>
            <div @click="deleteContact(index)" class="text-center pointer"><span class="fa fa-trash text-danger"></span></div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
  .pointer {
    cursor: pointer;
  }
</style>
