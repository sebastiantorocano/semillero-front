<template>
  <div>
    <div class="section" style="margin: 50px">
      <div class="row">
        <div class="col-sm-12 col-lg-6">
          <div>
            <h3>¿Quieres participar en el semillero?</h3>
            <button
              class="btn btn-outline-primary"
              style="margin:5px"
              data-toggle="modal"
              data-target="#preregistro"
            >Solicitar registro</button>
            <br />
            <br />
            <div class="col-12 col align-self-end row justify-content-start">
              <h4>Coordinador: {{coordinador[0].nombre_usuario}} {{coordinador[0].apellido_usuario}}</h4>
              <br />
              <br />

              <ul>
                <h3>Acerca del semillero {{semillero[0].semillero}}:</h3>
                <br />
                <h4>Objetivo</h4>
                <br />
                {{semillero[0].objetivo}}
                <br />
                <br />
                <h4>Información</h4>

                <br />
                {{semillero[0].descripcion}}
              </ul>
            </div>
          </div>
        </div>

        <!-- Opciones -->
        <div class="col-sm-12 col-lg-6">
          <ul class="nav nav-tabs col-12 row justify-content-center" id="myTab" role="tablist">
            <li class="nav-item">
              <a
                class="nav-link active"
                id="home-tab"
                data-toggle="tab"
                href="#home"
                role="tab"
                aria-controls="home"
                aria-selected="true"
              >Integrantes</a>
            </li>
            <li class="nav-item">
              <a
                class="nav-link"
                id="profile-tab"
                data-toggle="tab"
                href="#profile"
                role="tab"
                aria-controls="profile"
                aria-selected="false"
              >Proyectos</a>
            </li>
            <li class="nav-item">
              <a
                class="nav-link"
                id="contact-tab"
                data-toggle="tab"
                href="#contact"
                role="tab"
                aria-controls="contact"
                aria-selected="false"
              >Actividades</a>
            </li>
          </ul>

          <!-- <div class="row  justify-content-end"></div> -->
          <div class="tab-content" id="myTabContent">
            <div
              class="tab-pane fade show active"
              id="home"
              role="tabpanel"
              aria-labelledby="home-tab"
            >
              <template>
                <section class="content">
                  <div class="row">
                    <div class="col">
                      <div class="card">
                        <!-- /.card-header -->
                        <div class="card-body">
                          <section v-if="errored">
                            <p>Lo sentimos, no es posible obtener la información en este momento, por favor intente nuevamente mas tarde</p>
                          </section>
                          <section v-else>
                            <div v-if="loading">
                              cargando..
                              <div class="spinner-border text-success" role="status">
                                <span class="sr-only">Loading...</span>
                              </div>
                            </div>
                            <div v-else></div>
                            <div class="table-responsive">
                              <table
                                id="tblintegrantes"
                                class="table table-striped table-bordered dt-responsive nowrap"
                                style="width:100%"
                              >
                                <thead>
                                  <tr>
                                    <th>Nombre</th>
                                    <th>apellido</th>
                                    <th>Correo</th>
                                    <th>Tipo integrante</th>
                                  </tr>
                                </thead>
                                <tbody>
                                  <tr v-for="item in integrantes" :key="item.id_integrante">
                                    <td>{{ item.nombre_usuario }}</td>
                                    <td>{{ item.apellido_usuario }}</td>
                                    <td>{{ item.email }}</td>
                                    <td>{{item.tipo_usuario}}</td>
                                  </tr>
                                </tbody>
                              </table>
                            </div>
                          </section>
                        </div>
                        <!-- /.card-body -->
                      </div>
                    </div>
                  </div>
                </section>
              </template>
            </div>
            <!--  -->

            <!--  -->

            <div class="tab-pane fade" id="profile" role="tabpanel" aria-labelledby="profile-tab">
              <section class="content">
                <div class="row row justify-content-start">
                  <div class="col">
                    <div class="card">
                      <!-- /.card-header -->
                      <div class="card-body">
                        <section v-if="errored">
                          <p>Lo sentimos, no es posible obtener la información en este momento, por favor intente nuevamente mas tarde</p>
                        </section>
                        <section v-else>
                          <div v-if="loading">
                            cargando..
                            <div class="spinner-border text-success" role="status">
                              <span class="sr-only">Loading...</span>
                            </div>
                          </div>
                          <div v-else></div>
                          <div class="table-responsive">
                            <table
                              id="tblproyecto"
                              class="table table-striped table-bordered dt-responsive nowrap"
                              style="width:100%"
                            >
                              <thead>
                                <tr>
                                  <th>Nombre</th>
                                </tr>
                              </thead>
                              <tbody>
                                <tr v-for="item in proyectos" :key="item.id_proyecto">
                                  <td>{{ item.proyecto }}</td>
                                </tr>
                              </tbody>
                            </table>
                          </div>
                        </section>
                      </div>
                      <!-- /.card-body -->
                    </div>
                  </div>
                </div>
              </section>
            </div>
            <div class="tab-pane fade" id="contact" role="tabpanel" aria-labelledby="contact-tab">
              <section class="content">
                <div class="row row justify-content-start">
                  <div class="col">
                    <div class="card">
                      <!-- /.card-header -->
                      <div class="card-body">
                        <section v-if="errored">
                          <p>Lo sentimos, no es posible obtener la información en este momento, por favor intente nuevamente mas tarde</p>
                        </section>
                        <section v-else>
                          <div v-if="loading">
                            Cargando..
                            <div class="spinner-border text-success" role="status">
                              <span class="sr-only">Loading...</span>
                            </div>
                          </div>
                          <div v-else></div>
                          <div class="table-responsive">
                            <table
                              id="tblproyectos"
                              class="table table-striped table-bordered dt-responsive nowrap"
                              style="width:100%"
                            >
                              <thead>
                                <tr>
                                  <th>Nombre</th>
                                </tr>
                              </thead>
                              <tbody>
                                <tr v-for="item in actividades" :key="item.id_actividad">
                                  <td>{{ item.actividad }}</td>
                                </tr>
                              </tbody>
                            </table>
                          </div>
                        </section>
                      </div>
                      <!-- /.card-body -->
                    </div>
                  </div>
                </div>
              </section>
            </div>
            <div
              class="tab-pane fade"
              id="proyectos"
              role="tabpanel"
              aria-labelledby="proyectos-tab"
            >mixtape</div>
          </div>
        </div>
      </div>
    </div>

    <div
      class="modal fade"
      id="preregistro"
      tabindex="-1"
      role="dialog"
      aria-labelledby="exampleModalLabel"
      aria-hidden="true"
    >
      <div class="modal-dialog" role="document">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title" id="exampleModalLabel">Solicitud de registro</h5>
            <button type="button" class="close" data-dismiss="modal" aria-label="Close">
              <span aria-hidden="true">&times;</span>
            </button>
          </div>
        </div>
      </div>
      <div class="modal-body">
        <div style="width: 50%; margin: 0 auto;">
          <div class="card card-success">
            <form @submit.prevent="handleSubmit">
              <div class="card-body">
                <div class="form-group"></div>
                <label for="documento">Documento</label>
                <input
                  type="text"
                  pattern="[0-9]+"
                  title=" Solo números. Tamaño máximo: 12"
                  v-model.trim="usuario.documento"
                  id="documento"
                  name="documento"
                  placeholder="Documento"
                  class="form-control"
                  :class="{ 'is-invalid': submitted && $v.usuario.documento.$error }"
                />
                <div v-if="submitted && $v.usuario.documento.$error" class="invalid-feedback">
                  <span v-if="!$v.usuario.documento.required">El campo nombre es requerido</span>
                  <span
                    v-if="!$v.usuario.documento.maxLength"
                  >El nombre no debe superar los 50 caracteres</span>
                </div>
                <div class="form-group">
                  <label for="nombre_usuario">Nombre</label>
                  <input
                    type="text"
                    pattern="[A-Za-z ]+"
                    title=" Solo Letras. Tamaño máximo: 50"
                    v-model.trim="usuario.nombre_usuario"
                    id="nombre_usuario"
                    name="nombre_usuario"
                    placeholder="Nombre"
                    class="form-control"
                    :class="{ 'is-invalid': submitted && $v.usuario.nombre_usuario.$error }"
                  />
                  <div
                    v-if="submitted && $v.usuario.nombre_usuario.$error"
                    class="invalid-feedback"
                  >
                    <span v-if="!$v.usuario.nombre_usuario.required">El campo es requerido</span>
                    <span
                      v-if="!$v.usuario.nombre_usuario.maxLength"
                    >El campo no debe superar los 50 caracteres</span>
                  </div>
                </div>
                <div class="form-group">
                  <label for="apellido_usuario">Apellido</label>
                  <input
                    type="text"
                    pattern="[A-Za-z ]+"
                    title=" Solo Letras. Tamaño máximo: 50"
                    v-model.trim="usuario.apellido_usuario"
                    id="apellido_usuario"
                    name="apellido_usuario"
                    placeholder="Apellido"
                    class="form-control"
                    :class="{ 'is-invalid': submitted && $v.usuario.apellido_usuario.$error }"
                  />
                  <div
                    v-if="submitted && $v.usuario.apellido_usuario.$error"
                    class="invalid-feedback"
                  >
                    <span v-if="!$v.usuario.apellido_usuario.required">El campo es requerido</span>
                    <span
                      v-if="!$v.usuario.apellido_usuario.maxLength"
                    >El campo no debe superar los 50 caracteres</span>
                  </div>
                </div>
                <div class="form-group">
                  <label for="correo">Correo</label>
                  <input
                    type="text"
                    v-model.trim="usuario.email"
                    id="email"
                    name="email"
                    placeholder="Correo"
                    class="form-control"
                    :class="{ 'is-invalid': submitted && $v.usuario.email.$error }"
                  />
                  <div v-if="submitted && $v.usuario.email.$error" class="invalid-feedback">
                    <span v-if="!$v.usuario.email.required">El campo correo es requerido</span>
                    <span v-if="!$v.usuario.email">Email no Valido</span>
                    <span
                      v-if="!$v.usuario.email.maxLength"
                    >El campo no debe superar los 100 caracteres</span>
                  </div>
                </div>
                <div class="form-group">
                  <label for="telefono">Telefono</label>
                  <input
                    type="text"
                    pattern="[0-9]+"
                    title=" Solo Numeros. Tamaño máximo: 10"
                    v-model.trim="usuario.telefono"
                    id="telefono"
                    name="telefono"
                    placeholder="telefono"
                    class="form-control"
                    :class="{ 'is-invalid': submitted && $v.usuario.telefono.$error }"
                  />
                  <div v-if="submitted && $v.usuario.telefono.$error" class="invalid-feedback">
                    <span v-if="!$v.usuario.telefono.required">El campo es requerido</span>
                    <span
                      v-if="!$v.usuario.telefono.maxLength"
                    >El campo no debe superar los 10 caracteres</span>
                  </div>
                </div>
                <div class="card-footer">
                  <div class="modal-footer">
                    <button id="btn_modal" type="submit" class="btn btn-outline-success">Guardar</button>
                  </div>
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>
      <div class="modal-footer">
        <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
        <!--  <button type="button" class="btn btn-primary">Save changes</button> -->
      </div>
    </div>
  </div>
</template>

<script>
import { required, maxLength, email } from "vuelidate/lib/validators";
import ApiService from "../services/api.service";
import Swal from "sweetalert2/dist/sweetalert2.all.min.js";
export default {
  data() {
    return {
      loading: true,
      errored: false,
      integrantes: [],
      proyectos: [],
      semillero: {},
      actividades: [],
      usuario: {
        documento: "",
        nombre_usuario: "",
        apellido_usuario: "",
        email: "",
        telefono: "",
        tipo_usuario: "estudiante",
        id_semillero: this.$route.params.id
      },
      submitted: false,
      Tipos_Usuarios: {},
      coordinador: {}
    };
  },
  created() {
    ApiService.get(`/semillero/${this.$route.params.id}`).then(response => {
      if (response.status === 200) {
        /*  alert("No existen integrantes para mostrar "); */
        this.semillero = response.data;
        console.log(this.semillero);
      } else {
        console.log("nada");
      }
    });

    ApiService.get(`/coordinador/semillero/${this.$route.params.id}`).then(response => {
      if (response.status === 200) {
        /*  alert("No existen integrantes para mostrar "); */
        this.coordinador = response.data;
        console.log(this.coordinador);
      } else {
        console.log("nada");
      }
    });

    ApiService.get(`/integrante/semillero/actual/${this.$route.params.id}`)
      .then(response => {
        if (response.status === 204) {
          /*  alert("No existen integrantes para mostrar "); */
          this.integrantes = response.data;
        } else {
          this.integrantes = response.data;
        }
      })
      .then(res => {
        $("#tblintegrantes").DataTable({
          responsive: true,
          retrieve: true
        });
      })
      .catch(error => {
        console.log(error);
        this.errored = true;
      })
      .finally(() => (this.loading = false));

    ApiService.get(`/actividad/semillero/actual/${this.$route.params.id}`)
      .then(response => {
        if (response.status === 204) {
          this.actividades = response.data;
        } else {
          this.actividades = response.data;
        }
      })
      .then(res => {
        $("#tblactividad").DataTable({
           language: {
            url: "//cdn.datatables.net/plug-ins/1.10.15/i18n/Spanish.json"
          },
          responsive: true,
          retrieve: true
        });
      })
      .catch(error => {
        console.log(error);
        this.errored = true;
      })
      .finally(() => (this.loading = false));

    ApiService.get(`/proyecto/semillero/actual/${this.$route.params.id}`)
      .then(response => {
        if (response.status === 204) {
          this.proyectos = response.data;
        } else {
          this.proyectos = response.data;
        }
      })
      .then(res => {
        $("#tblproyectos").DataTable({
          responsive: true,
          retrieve: true
        });
      })
      .catch(error => {
        console.log(error);
        this.errored = true;
      })
      .finally(() => (this.loading = false));
  },
  //Obtiene las tipos de usuarios una vez se llama al componente
  mounted() {
    this.getTipos_Usuarios();
  },
  //comvierte el objeto->en un arreglo
  computed: {
    formatearTipos_Usuarios() {
      return Object.values(this.Tipos_Usuarios);
    }
  },
  //Reglas de validacion para VueValidate
  validations: {
    usuario: {
      documento: { required, maxLength: maxLength(12) },
      nombre_usuario: { required, maxLength: maxLength(50) },
      apellido_usuario: { required, maxLength: maxLength(50) },
      email: { required, email, maxLength: maxLength(100) },
      telefono: { required, maxLength: maxLength(10) }
    }
    /* grupo: {
      id_grupo: { required }
    } */
  },
  methods: {
    enviarPreregistro() {
      ApiService.post("/semillero/solicitud", this.usuario).then(response => {
        console.log(response.data);
        console.log(response.status);
        if (response.status === 200) {
          this.$swal({
            type: "success",
            text: "La solicitud ha sido enviada",
            timer: 2000,
            showCancelButton: false,
            showConfirmButton: false
          });
          $("#preregistro ").modal("hide");
        }
      });
    },
    getTipos_Usuarios() {
      ApiService.get("/tipousuario").then(response => {
        this.Tipos_Usuarios = response.data;
      });
    },
    selectChangeTipoUsuario(event) {
      var i;
      this.Tipos_Usuarios.forEach(function(element) {
        if (element.tipo_usuario == event.target.value) {
          i = element.id_tipo_usuario;
        }
      });
      this.usuario.id_tipo_usuario = i;
    },
    //Valida el formulario
    handleSubmit(e) {
      this.submitted = true;

      // Se detiene aqui si es invalido, de lo contrario ejecuta el submit()
      this.$v.$touch();
      if (this.$v.$invalid) {
        return;
      }

      this.enviarPreregistro();
      /* alert("SUCCESS!! :-)\n\n" + JSON.stringify(this.grupo)); */
    }
  }
};
</script>