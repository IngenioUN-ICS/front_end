<template>
  <div class="col-12 col-sm-12 col-md-12 col-lg-12 col-xl-12">
    <table class="table table-hover table-bordered" aria-describedby="Author requestes Table">
      <thead class="thead-light">
        <tr>
          <th scope="col">#</th>
          <th scope="col">Name</th>
          <th scope="col">LastName</th>
          <th scope="col">Publications</th>
        </tr>
      </thead>
      <tbody v-for="(item,index) of items" :key="item.id">
        <tr>
          <th scope="row">{{index + 1}} </th>
          <td>
            <a data-toggle="modal" >
              {{item.firstName}}
            </a>
          </td>
          <td>
            <a data-toggle="modal" >
              {{item.lastName}}
            </a>
          </td>
          <td>
            <a data-toggle="modal" >
              {{item.myPublications.length}}
            </a>
          </td>
        </tr>
      </tbody>
    </table>
    <div class="modal fade" id="MoreInfoUser" tabindex="-1" role="dialog" aria-labelledby="MoreInfoUserModalLabel" aria-hidden="true">
      <div class="modal-dialog modal-md modal-dialog-scrollable" role="document" >
        <div class="modal-content">
          <div class="modal-header bg-light">
          <h1 class="modal-title" id="MoreInfoUserModal"><em>User Information</em></h1>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close" >
            <span aria-hidden="true" >&times;</span>
          </button>
          </div>
          <div class="modal-body bg-light container" >
            <MoreInfoUser  :email2="datoPasar.email2" :pC="datoPasar.professionalCard" :eH="datoPasar.employmentHistory" :aH="datoPasar.academicHistory"/>
            </div>
          <div class="modal-footer bg-light">
            Terms y Conditions
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
axios.defaults.withCredentials = true;
import MoreInfoUser from '../components/MoreInfoUser.vue';

export default {
  name: 'Authors.vue',
  components: {
    MoreInfoUser
  },
  data(){
    return {
      disabled:0,
      datoPasar : [],
      items: [],
    };
  },
  mounted() {
    this.getAuthors();
  },
  methods:{
    getAuthors() {
      axios
      .get(this.$store.state.backURL + "/user/get-authors")
      .then(response => {
        this.items = response.data;
      })
      .catch( error => {
        console.log( "¡Parece que hubo un error de comunicación con el servidor!" );
      });
    }
  }
}
</script>
