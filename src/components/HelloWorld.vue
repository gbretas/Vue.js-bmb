<script type="module">
  import axios from 'axios'
  import {
    responseData
  } from '../data.js'

  export default {
    data() {
      return {
        details: [],
        details1: [],
        details2: [],
        details3: [],
        details4: [],
        details5: [],
        details6: [],
        CS_DATA_LIST: [],
        filterResults: [],
        SCHOLARSHIPS: [],
        newData: [],
        filterActive: false,
        mode: ['Ver Todos'],
        shift: ['Ver Todos'],
        course: ['Ver Todos'],
        mode1: [],
        shift1: [],
        course1: [],
        units: [],
        modeValue: [],
        shiftValue: [],
        status: Boolean = false,
        selectedMode: {
          content_modality: {
            name: ''
          },
          content_shift: {
            name: ''
          },
          content_type: {
            name: ''
          }
        }
      }
    },
    computed: {
      sortedCategories() {

      }

    },
    methods: {
      getData() {
        this.details = responseData.scholarships
        // this.details5 = responseData.scholarships
        // // console.log(this.details1)
        responseData.scholarships.map(async (t) => {
            if ((this.SCHOLARSHIPS.push(t), this.CS_DATA_LIST.length > 0)) {
              let e = this.CS_DATA_LIST.find((e) => e.course.name === t.course.name && e.school.name === t.school
                .name);

              if (null == e) {
                let e = {
                  course: t.course,
                  school: t.school,
                  content_level: t.content_level,
                  modalities: [],
                  shifts: [],
                  units: [],
                  scholarships: []
                };
                this.CS_DATA_LIST.push(e);
              }
            } else {
              let e = {
                course: t.course,
                school: t.school,
                content_level: t.content_level,
                modalities: [],
                shifts: [],
                units: [],
                scholarships: []
              };
              this.CS_DATA_LIST.push(e);
            }
          }),

          responseData.scholarships.map(async (t) => {
            const e = await t;
            var shifts = [],
              modalities = [],
              units = []
            for (let t = 0; t < this.CS_DATA_LIST.length; t++) {
              this.CS_DATA_LIST[t].course.name === e.course.name && this.CS_DATA_LIST[t].school.name === e.school
                .name && this.CS_DATA_LIST[t].content_level.name === e.content_level.name && this.CS_DATA_LIST[t]
                .scholarships.push(e);
            }
          });

        this.details = this.CS_DATA_LIST
        this.getMode()

      },
      getData1() {
        responseData.scholarships.map(async (t) => {
            if ((this.SCHOLARSHIPS.push(t), this.details5.length > 0)) {
              let e = this.details5.find((e) => e.course.name === t.course.name && e.school.name === t.school.name);

              if (null == e) {
                let e = {
                  course: t.course,
                  school: t.school,
                  content_level: t.content_level,
                  modalities: [],
                  shifts: [],
                  units: [],
                  scholarships: []
                };
                this.details5.push(e);
              }
            } else {
              let e = {
                course: t.course,
                school: t.school,
                content_level: t.content_level,
                modalities: [],
                shifts: [],
                units: [],
                scholarships: []
              };
              this.details5.push(e);
            }
          }),

          responseData.scholarships.map(async (t) => {
            const e = await t;
            var shifts = [],
              modalities = [],
              units = []
            for (let t = 0; t < this.details5.length; t++) {
              this.details5[t].course.name === e.course.name && this.details5[t].school.name === e.school.name &&
                this.details5[t].content_level.name === e.content_level.name && this.details5[t].scholarships.push(
                  e);

            }
          });
        this.details3 = this.details5
        // // console.log(this.details3)
        // this.getMode()

      },
      async getMode() {
        responseData.scholarships.map((mode, index) => {
          this.mode.push(mode.content_modality.name)
          this.units.push(mode.unit.name)
          this.shift.push(mode.content_shift.name)
          this.course.push(mode.content_type.name)
          this.mode1.push(mode.content_modality.name)
          this.shift1.push(mode.content_shift.name)

        })

        let unique_mode = [...new Set(this.mode)]
        let unique_shift = [...new Set(this.shift)]
        let unique_course = [...new Set(this.course)]
        let unique_mode1 = [...new Set(this.mode1)]
        let unique_shift1 = [...new Set(this.shift1)]
        let units = [...new Set(this.units)]
        this.mode = unique_mode;
        this.shift = unique_shift;
        this.course = unique_course
        this.mode1 = unique_mode1;
        this.shift1 = unique_shift1;
        this.units = units;

        for (var i = 0; i < this.CS_DATA_LIST.length; i++) {
          this.getModalities(await this.CS_DATA_LIST[i].scholarships, i)
          this.getShifts(await this.CS_DATA_LIST[i].scholarships, i)
          this.getUnitss(await this.CS_DATA_LIST[i].scholarships, i)

        }
      },
      getModalities(t, index) {
        let e = "",
          a = [];

        t.map((t) => {
          if (a.length > 0) {
            let e = a.find((e) => e.id === t.content_modality.id);
            null == e && a.push(t.content_modality);
          } else a.push(t.content_modality);
        })
        this.CS_DATA_LIST[index].modalities.push(...a)
      },
      getShifts(t, index) {
        let e = "",
          a = [];

        t.map((t) => {
          if (a.length > 0) {
            let e = a.find((e) => e.id === t.content_shift.id);
            null == e && a.push(t.content_shift);
          } else a.push(t.content_shift);
        })

        this.CS_DATA_LIST[index].shifts.push(...a)
        // // console.log(this.CS_DATA_LIST)
      },
      getUnitss(t, index) {
        let e = "",
          a = [];

        t.map((t) => {
          if (a.length > 0) {
            let e = a.find((e) => e.id === t.unit.id);
            null == e && a.push(t.unit);
          } else a.push(t.unit);
        })

        this.CS_DATA_LIST[index].units.push(...a)

      },
      changeModalities(data1, index) {
        var filterData = {
          scholarships: []
        }


        var filter1 = []
        filter1 = this.details5
        this.CS_DATA_LIST[index].scholarships = this.details5[index].scholarships
        this.modeValue = []
        this.modeValue.push(data1.name)
        // // console.log(this.CS_DATA_LIST)
        if (this.filterActive == false) {
          this.CS_DATA_LIST[index].scholarships.filter((data, index) => {
            // // console.log('i am here',data)
            if (data.content_modality.name == data1.name) {
              return filterData.scholarships.push(data)
            }
          })
          this.CS_DATA_LIST[index]['scholarships'] = filterData.scholarships
          this.details = filterData.scholarships
        } else {
          this.filterResults[index].scholarships.filter((data, index) => {
            // // console.log('i am here',data)
            if (data.content_modality.name == data1.name) {
              return filterData.scholarships.push(data)
            }
          })
          this.filterResults[index]['scholarships'] = filterData.scholarships
          this.details = filterData.scholarships
        }
        // console.log('filterData', this.details)


      },
      changeShifts(data2, index) {
        var filterData = []
        var filter1 = []
        this.shiftValue = []
        this.shiftValue.push(data2.name)
        // console.log(this.CS_DATA_LIST, index)
        if (this.filterActive == false) {
          if (this.modeValue.length == 0) {
            alert('selecione a modalidade')
          } else {
            // console.log(this.CS_DATA_LIST)
            this.CS_DATA_LIST[index].scholarships.filter((data, index) => {
              if (data.content_shift.name == data2.name && data.content_modality.name == this.modeValue[0]) {
                return filterData.push(data)

              }
            })
            // console.log(filterData)
            this.CS_DATA_LIST[index]['scholarships'] = filterData
            this.details5 = this.CS_DATA_LIST[index]['scholarships']
            // console.log(this.details5)
            // this.details=filterData;
          }
        } else {
          if (this.modeValue.length == 0) {
            alert('selecione a modalidade')
          } else {
            this.filterResults[index].scholarships.filter((data, index) => {
              if (data.content_shift.name == data2.name && data.content_modality.name == this.modeValue[0]) {
                return filterData.push(data)

              }
            })
            // console.log(filterData)
            this.filterResults[index]['scholarships'] = filterData
            this.details5 = this.filterResults[index]['scholarships']
            // console.log(this.details5)
            // this.details=filterData;
          }
        }
      },
      changeUnits(data3, index) {
        var filterData = []
        var filter1 = []
        filter1 = this.details
        delete filter1.scholarships
        this.CS_DATA_LIST[index].scholarships = filter1
        // console.log(this.CS_DATA_LIST, index)
        if (this.filterActive == false) {
          if (this.modeValue.length == 0) {
            alert('selecione a modalidade')
          } else {
            // console.log(this.CS_DATA_LIST)
            this.CS_DATA_LIST[index].scholarships.filter((data, index) => {
              if (data.unit.name == data3.name && data.content_modality.name == this.modeValue[0] && data
                .content_shift.name == this.shiftValue[0]) {
                return filterData.push(data)

              }
            })
            // console.log(filterData)
            this.CS_DATA_LIST[index]['scholarships'] = filterData
            this.details5 = this.CS_DATA_LIST[index]['scholarships']
            // console.log(this.details5.length)
            // this.details=filterData;
          }
        } else {
          if (this.modeValue.length == 0) {
            alert('selecione a modalidade')
          } else {
            // console.log(this.filterResults)
            this.filterResults[index].scholarships.filter((data, index) => {
              if (data.unit.name == data3.name && data.content_modality.name == this.modeValue[0] && data
                .content_shift.name == this.shiftValue[0]) {
                return filterData.push(data)

              }
            })
            // console.log(filterData)
            this.filterResults[index]['scholarships'] = filterData
            this.details5 = this.filterResults[index]['scholarships']
            // console.log(this.details5.length)
            // this.details=filterData;
          }
        }
      },
      //this one 
      modeChange(event) {
        this.filterActive = true;
        this.filterResults = JSON.parse(JSON.stringify(this.CS_DATA_LIST));

        // console.log(this.filterResults)


        if (event.target.value != 'Ver Todos') {

          this.filterResults.map((t, index) => {
            var scholarships = this.filterScholarships(t.scholarships);
            // // console.log(scholarships)        
            if (scholarships.length > 0) {
              this.filterResults[index]['scholarships'] = scholarships
            } else {
              this.filterResults[index]['scholarships'] = []
            }
          });
          // console.log(this.filterResults)
          // this.CS_DATA_LIST=filterResults
        }

      },
      filterScholarships(scholarships) {
        var filteredScholarships = scholarships.filter((el) => {
          const flag = this.filterArray(el)
          return flag < 0 ? true : false
        });

        return filteredScholarships
      },

      filterArray(element, ) {
        var flagArray = []
        for (const [key, value] of Object.entries(this.selectedMode)) {
          for (const [key1, value1] of Object.entries(value)) {
            if (this.selectedMode[key][key1] != '') {
              flagArray.push(this.selectedMode[key][key1] == element[key][key1])
            }
          }
        }
        return flagArray.indexOf(false)

      },
      async modeChange1(event) {
        // console.log(this.details6)
        let dataValue = []
        let filterData = [];
        dataValue = this.details6
        // console.log(dataValue)

        if (event.target.value != 'Ver Todos') {

          this.filterResults.map((t, index) => {
            var scholarships = this.filterScholarships(t.scholarships);
            // // console.log(scholarships)        
            if (scholarships.length > 0) {
              this.filterResults[index]['scholarships'] = scholarships
            } else {
              this.filterResults[index]['scholarships'] = []
            }
          });

        } else {
          this.details = this.details4
          // console.log(this.details)

        }
      },

    },
    mounted() {
      this.getData()
      this.getData1()

      // para cada uma das bolsas
        // para modalidades
        // para turnos
        // para unidades

    //for this.filterResults[index].scholarships
    // console.log("sadas")
   this.CS_DATA_LIST.forEach((schl) => {
    console.log(schl.toRaw())

      schl.modalities.forEach((schlSchl) => {
        console.log(schlSchl)
        // this.modalities.push(schlSchl.content_modality.name)
        // this.shifts.push(schlSchl.content_shift.name)
        // this.units.push(schlSchl.unit.name)
      })
    })
    }
  }
</script>

<template>
  <div class="container-fluid">
    <div class="row mb-5">
      <div class="col-md-3">
        <div class="card institution">
          <div class="card-body">
            <form>
              <label>Institui????o</label>
              <select class="form-select mb-3" aria-label="Default select example">
                <option selected>Open this select menu</option>
              </select>
              <label>Encontre um Curso:</label>
              <select class="form-select mb-3" aria-label="Default select example">
                <option selected>Open this select menu</option>
              </select>
              <label>Cidade:</label>
              <select class="form-select mb-3" aria-label="Default select example">
                <option selected>Open this select menu</option>
              </select>
              <!-- Button to search again -->
              <button type="button" class="btn btn-primary">Buscar</button>
              <br />
              <hr />
              <label class="mb-3">Modalidade: </label> <br />
              <div v-for="data in mode" :key='data'>
                <input type="radio" name="test_id1" v-model="selectedMode.content_modality.name"
                  @change="modeChange($event)" v-bind:value="data"> {{ data }}
              </div>
              <br />
              <label class="mb-3">Turno:</label> <br />
              <div v-for="data in shift" :key='data'>
                <input type="radio" name="test_id2" v-model="selectedMode.content_shift.name"
                  @change="modeChange($event)" v-bind:value="data"> {{ data }}
              </div>
              <br />
              <label>N??vel de Curso:</label>
              <select class="form-select mb-3" aria-label="N??vel do Curso">
                <option selected>Selecionar</option>
              </select>
              <label>??rea de Estudo:</label>
              <select class="form-select mb-3" aria-label="??rea de Estudo">
                <option selected>Selecionar</option>
              </select>
              <label class="mb-3">Tipo de Curso:</label>
              <div v-for="data in course" :key='data'>
                <input type="radio" name="test_id3" v-model="selectedMode.content_type.name"
                  @change="modeChange($event)" v-bind:value="data"> {{ data
                }}
              </div>
            </form>
          </div>
        </div>
      </div>
      <div class="col-md-9" v-if="CS_DATA_LIST.length == 0">
        <div class="card institution">
          <div class="card-body">
            <div class="row">
              <div class="col-md-3">
                <div>
                  <img :src="details.school?.image" height="100" class="imagess" />
                  <div class="text-center mb-4">
                    <h3>{{ details.school?.name }}</h3>
                  </div>
                  <!-- <div v-html="data.more_bonus_text_button">
                  </div> -->

                </div>
              </div>
              <div class="col-md-9 ead">
                <h3>{{ details.course?.name }}</h3>
                <div>
                  <label class="mt-3">Modalities:</label> <br />

                  <div class="btn-group" role="group" aria-label="Basic checkbox toggle button group">
                    <div v-for="data in mode1" :key='data' class="mx-1">
                      <input type="radio" class="btn-check" name="btnradio" v-bind:id="data" autocomplete="off">
                      <label class="btn btn-outline-success btn-sm" v-bind:for="data" @click="changeModalities(data)">{{
                          data
                      }}</label>
                    </div>
                  </div>

                  <br />
                  <label class="mt-3">Shifts :</label> <br />
                  <div class="btn-group" role="group" aria-label="Basic checkbox toggle button group">
                    <div v-for="data in shift1" :key='data' class="mx-1">
                      <input type="radio" class="btn-check" name="btnradio1" v-bind:id="data" autocomplete="off">
                      <label class="btn btn-outline-success btn-sm" v-bind:for="data"
                        @click="changeShifts(data, index)">{{
                            data
                        }}</label>
                    </div>
                  </div>
                  <br />
                  <label class="mt-3">Units:</label> <br />
                  <div class="btn-group units" role="group" aria-label="Basic checkbox toggle button group"
                    style="flex-wrap:wrap">
                    <div v-for="data in units" :key='data' class="mx-1">
                      <input type="radio" class="btn-check" name="btnradio2" v-bind:id="data" autocomplete="off">
                      <label class="btn btn-outline-success btn-sm" v-bind:for="data" @click="changeUnits(data, index)">{{ data
                        }}</label>
                    </div>
                  </div>

                </div>
              </div>
            </div>

            <div class="my-4">
              <hr />
            </div>
            <div v-if="details.length != 0">
              <div class="payment" v-for="data in details.scholarships" :key='data'>
                <div class="row">
                  <div class="col-md-9">
                    <div class="row">
                      <div class="col-md-3">
                        <p>Modalidade: <b> {{ data?.content_modality?.name }} </b><br />
                          Turno:<b> {{ data?.content_shift?.name }} </b><br />
                          Unidade:<b>{{ data?.unit?.name }} </b></p>
                      </div>
                      <div class="col-md-3">
                        <p>Type: <b> {{ data?.content_type?.name }} </b><br />
                          Dura????o: <br /> <b>{{ data?.duration }} {{ data?.duration_type }} </b><br />
                          Parcelas:<b> {{ data?.discount_installments }} </b></p>
                      </div>
                      <div class="col-md-3">
                        <p class="p-0">Mensalidade: <br />
                          <span class="frombrl">De R$ {{ data?.original_price }}</span><br />
                          Por<br /> <b> <span class="brl"><span>R$ </span><span>R$
                              </span>{{ data?.comission_amount }}</span> </b>
                        </p>
                        <!-- <small class="text-center">8785865 VB163.28 - 100</small> -->
                      </div>
                      <div class="col-md-3">
                        <p>Bolsa: <b> {{ data?.percent }}%</b> <br />
                          Economia Total:<br />
                          <b> <span class="brl"><span>R$ </span></span> {{ data?.economy_total }} </b>
                        </p>
                      </div>
                    </div>
                  </div>
                  <div class="col-md-3 text-center">
                    <a href="#">Ver Detalhes</a> <br />
                    <button class="btn btn-success btn-sm" type="button">Escolha Esta Bolsa</button>
                  </div>
                </div>
              </div>
            </div>
            <div v-if="details.length == 0">
              <p>N??o h?? bolsas dispon??veis com os itens selecionados, mude a unidade, turno ou modalidade selecionada.
              </p>
            </div>
          </div>
        </div>
        <!-- <div class="my-4">
        <nav aria-label="Page navigation example">
          <ul class="pagination">
            <li class="page-item"><a class="page-link" href="#">Previous</a></li>
            <li class="page-item"><a class="page-link" href="#">1</a></li>
            <li class="page-item"><a class="page-link" href="#">2</a></li>
            <li class="page-item"><a class="page-link" href="#">3</a></li>
            <li class="page-item"><a class="page-link" href="#">Next</a></li>
          </ul>
        </nav>
        </div> -->
      </div>

      <div class="col-md-9" v-if="!filterActive">
        <div v-if="CS_DATA_LIST.length > 0">
          <div class="card institution" v-for="(data, index) in CS_DATA_LIST" :key='data'>
            <div class="card-body">
              <div class="row">
                <div class="col-md-3">
                  <div>
                    <img :src="data.school?.image" height="100" class="imagess" />
                    <div class="text-center mb-4">
                      <h3>{{ data.school?.name }}</h3>
                    </div>
                    <!-- <div v-html="data.more_bonus_text_button">
                  </div> -->

                  </div>
                </div>
                <div class="col-md-9 ead">
                  <h3>{{ data.course?.name }}</h3>
                  <div>
                    <label class="mt-3">Modalidades:</label> <br />

                    <div class="btn-group modalidades" role="group">

                      <div v-for="data in data.modalities" :key='data' class="mx-1">
                        <input type="radio" class="btn-check" name="btnradio" v-bind:id="data.name + index" autocomplete="off"  v-bind:selected="index === 0">
                        <label class="btn btn-outline-success btn-sm" v-bind:for="data.name + index"
                          @click="changeModalities(data, index)">{{data.name}}</label>
                      </div>



                    </div>

                    <br />
                    <label class="mt-3">Turnos:</label> <br />
                    <div class="btn-group" role="group" aria-label="Basic checkbox toggle button group">
                      <div v-for="data in data.shifts" :key='data' class="mx-1">
                        <input type="radio" class="btn-check" name="btnradio1" v-bind:id="data.name + index"
                          autocomplete="off">
                        <label class="btn btn-outline-success btn-sm" v-bind:for="data.name + index"
                          @click="changeShifts(data, index)">{{
                            data.name
                        }}</label>
                      </div>
                    </div>
                    <br />
                    <label class="mt-3">Unidades:</label> <br />
                    <div class="btn-group units" role="group" aria-label="Basic checkbox toggle button group"
                      style="flex-wrap:wrap">


                      <div v-for="data in data.units" :key='data' class="mx-1">

                        <input type="radio" class="btn-check" name="btnradio2" v-bind:id="data.name + index" autocomplete="off">
                        <label class="btn btn-outline-success btn-sm" v-bind:for="data.name + index" @click="changeUnits(data, index)">{{ data.name}}</label>

                      </div>


                    </div>

                    <div class="btn-group units2" role="group" aria-label="Basic checkbox toggle button group" style="flex-wrap:wrap" v-if="data.units.length > 2">
                      > 2
                      <!-- for > 2 -->
                      <div v-for="(dataunit, index2) in data.units" :key='data' class="mx-1">

                        <input type="radio" class="btn-check" name="btnradio2" v-bind:id="dataunit.name + index + 2" autocomplete="off">
                        <label class="btn btn-outline-success btn-sm" v-bind:for="dataunit.name + index" @click="changeUnits(data, index)">{{ dataunit.name}}</label>

                      </div>


                    </div>

                  </div>
                </div>
              </div>

              <div class="my-4">
                <hr />
              </div>
              <div>
                <div v-if="data.scholarships.length > 0">
                  <div class="payment" v-for="data1 in data.scholarships" :key='data1'>
                    <div class="row">
                      <div class="col-md-9">
                        <div class="row">
                          <div class="col-md-3">
                            <p>Modalidade: <b> {{ data1?.content_modality?.name }} </b><br />
                              Turno:<b> {{ data1?.content_shift?.name }} </b><br />
                              Unidade:<b>{{ data1?.unit?.name }} </b></p>
                          </div>
                          <div class="col-md-3">
                            <p>Type: <b> {{ data1?.content_type?.name }} </b><br />
                              Dura????o: <br /> <b>{{ data1?.duration }} {{ data1?.duration_type }} </b><br />
                              Parcelas:<b> {{ data1?.discount_installments }} </b></p>
                          </div>
                          <div class="col-md-3">
                            <p class="p-0">Mensalidade: <br />
                              <span class="frombrl">De R$ {{ data1?.original_price }}</span><br />
                              Por<br /> <b> <span class="brl"><span>R$ </span>{{ data1?.comission_amount }}</span> </b>
                            </p>
                            <!-- <small class="text-center">8785865 VB163.28 - 100</small> -->
                          </div>
                          <div class="col-md-3">
                            <p>Bolsa: <b> {{ data1?.percent }}%</b> <br />
                              Economia Total:<br />
                              <b> <span class="brl"><span>R$ </span></span> {{ data1?.economy_total }} </b>
                            </p>
                          </div>
                        </div>
                      </div>
                      <div class="col-md-3 text-center">
                        <a href="#">Ver Detalhes</a> <br />
                        <button class="btn btn-success btn-sm" type="button">Escolha Esta Bolsa</button>
                      </div>
                    </div>
                  </div>
                </div>
                <div v-if="data.scholarships.length == 0">
                  <p>N??o h?? bolsas dispon??veis com os itens selecionados, mude a unidade, turno ou modalidade
                    selecionada.
                  </p>
                </div>
              </div>

            </div>
          </div>
          <!-- <div class="my-4">
        <nav aria-label="Page navigation example">
          <ul class="pagination">
            <li class="page-item"><a class="page-link" href="#">Previous</a></li>
            <li class="page-item"><a class="page-link" href="#">1</a></li>
            <li class="page-item"><a class="page-link" href="#">2</a></li>
            <li class="page-item"><a class="page-link" href="#">3</a></li>
            <li class="page-item"><a class="page-link" href="#">Next</a></li>
          </ul>
        </nav>
        </div> -->
        </div>
      </div>

      <div class="col-md-9" v-if="filterActive">
        <div v-if="filterResults.length > 0">
          <div class="card institution" v-for="(data, index) in filterResults" :key='data'>
            <div class="card-body" v-if="data.scholarships.length>0">
              <div class="row">
                <div class="col-md-3">
                  <div>
                    <img :src="data.school?.image" height="100" class="imagess" />
                    <div class="text-center mb-4">
                      <h3>{{ data.school?.name }}</h3>
                    </div>
                    <!-- <div v-html="data.more_bonus_text_button">
                  </div> -->

                  </div>
                </div>
                <div class="col-md-9 ead">
                  <h3>{{ data.course?.name }}</h3>
                  <div>
                    <label class="mt-3">Modalities:</label> <br />

                    <div class="btn-group" role="group" aria-label="Basic checkbox toggle button group">
                      <div v-for="data in data.modalities" :key='data' class="mx-1">
                        <input type="radio" class="btn-check" name="btnradio" v-bind:id="data.name + index"
                          autocomplete="off">
                        <label class="btn btn-outline-success btn-sm" v-bind:for="data.name + index"
                          @click="changeModalities(data, index)">{{
                            data.name
                        }}</label>
                      </div>
                    </div>

                    <br />
                    <label class="mt-3">Shifts :</label> <br />
                    <div class="btn-group" role="group" aria-label="Basic checkbox toggle button group">
                      <div v-for="data in data.shifts" :key='data' class="mx-1">
                        <input type="radio" class="btn-check" name="btnradio1" v-bind:id="data.name + index"
                          autocomplete="off">
                        <label class="btn btn-outline-success btn-sm" v-bind:for="data.name + index"
                          @click="changeShifts(data, index)">{{
                            data.name
                        }}</label>
                      </div>
                    </div>
                    <br />
                    <label class="mt-3">Unidades:</label> <br />


                    <div class="btn-group units" role="group" aria-label="Basic checkbox toggle button group"
                      style="flex-wrap:wrap">
                      <div v-for="data in data.units" :key='data' class="mx-1">
                        <input type="radio" class="btn-check" name="btnradio2" v-bind:id="data.name + index"
                          autocomplete="off">
                        <label class="btn btn-outline-success btn-sm" v-bind:for="data.name + index"
                          @click="changeUnits(data, index)">{{ data.name
                        }}</label>
                      </div>
                    </div>

                    

                  </div>
                </div>
              </div>

              <div class="my-4">
                <hr />
              </div>
              <div>
                <div v-if="data.scholarships.length > 0">
                  <div class="payment" v-for="data1 in data.scholarships" :key='data1'>
                    <div class="row">
                      <div class="col-md-9">
                        <div class="row">
                          <div class="col-md-3">
                            <p>Modalidade: <b> {{ data1?.content_modality?.name }} </b><br />
                              Turno:<b> {{ data1?.content_shift?.name }} </b><br />
                              Unidade:<b>{{ data1?.unit?.name }} </b></p>
                          </div>
                          <div class="col-md-3">
                            <p>Type: <b> {{ data1?.content_type?.name }} </b><br />
                              Dura????o: <br /> <b>{{ data1?.duration }} {{ data1?.duration_type }} </b><br />
                              Parcelas:<b> {{ data1?.discount_installments }} </b></p>
                          </div>
                          <div class="col-md-3">
                            <p class="p-0">Mensalidade: <br />
                              <span class="frombrl">De R$ {{ data1?.original_price }}</span><br />
                              Por<br /> <b> <span class="brl"><span>R$ </span>{{ data1?.comission_amount }}</span> </b>
                            </p>
                            <!-- <small class="text-center">8785865 VB163.28 - 100</small> -->
                          </div>
                          <div class="col-md-3">
                            <p>Bolsa: <b> {{ data1?.percent }}%</b> <br />
                              Economia Total:<br />
                              <b> <span class="brl"><span>R$ </span></span> {{ data1?.economy_total }} </b>
                            </p>
                          </div>
                        </div>
                      </div>
                      <div class="col-md-3 text-center">
                        <a href="#">Ver Detalhes</a> <br />
                        <button class="btn btn-success btn-sm" type="button">Escolha Esta Bolsa</button>
                      </div>
                    </div>
                  </div>
                </div>
                <div v-if="data.scholarships.length == 0">
                  <p>N??o h?? bolsas dispon??veis com os itens selecionados, mude a unidade, turno ou modalidade
                    selecionada.
                  </p>
                </div>
              </div>

            </div>
          </div>
          <!-- <div class="my-4">
        <nav aria-label="Page navigation example">
          <ul class="pagination">
            <li class="page-item"><a class="page-link" href="#">Previous</a></li>
            <li class="page-item"><a class="page-link" href="#">1</a></li>
            <li class="page-item"><a class="page-link" href="#">2</a></li>
            <li class="page-item"><a class="page-link" href="#">3</a></li>
            <li class="page-item"><a class="page-link" href="#">Next</a></li>
          </ul>
        </nav>
        </div> -->
        </div>
      </div>
    </div>

  </div>

</template>

<style scoped>
  h1 {
    font-weight: 500;
    font-size: 2.6rem;
    top: -10px;
  }

  span.brl {
    /* font-size: 1.83em; */
    color: #21293e;
    font-weight: bold;
  }

  h3 {
    font-size: 1.2rem;
  }

  span.frombrl {
    text-decoration: line-through;
  }

  .btn-group.units div,   .btn-group.units2 div {
    margin: 5px;
  }

  .btn-group.units div:nth-child(n+4) {
    display: none;
  }
</style>