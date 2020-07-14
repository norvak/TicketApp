<template>
  <v-container
    v-if="valid"
    id="dashboard"
    fluid
    tag="section"
  >
    <!-- Checks -->
    <v-card
      style="max-height: 200px; background-image: linear-gradient(to right top, #81d0ce, #71c7c5, #5fbebb, #4db5b2, #37aca9, #37aca9, #37aca9, #37aca9, #4db5b2, #5fbebb, #71c7c5, #81d0ce);"
      class="overflow-y-auto pa-4"
      max-width="100%"
    >
      <v-row
        align="center"
      >
        <v-col
          v-for="(item, i) in mapTitles"
          :key="i"
          md="3"
        >
          <v-switch
            v-model="filterItems"
            :label="item.title"
            :value="item"
            color="black"
            dense
          />
        </v-col>
      </v-row>
    </v-card>
    <!-- Selection list -->
    <v-row>
      <v-col
        cols="12"
        md="3"
        class="no-padding-column-selection"
      >
        <v-col
          v-for="(item, i) in selectFilter"
          :key="item.title"
          cols="12"
          md="12"
          class="no-padding"
        >
          <!-- <v-divider /> -->
          <v-card
            class="v-card--wizard no-margin is-selected mb-2 overflow-x-auto"
            style="background-image: linear-gradient(to right top, #81d0ce, #71c7c5, #5fbebb, #4db5b2, #37aca9, #37aca9, #37aca9, #37aca9, #4db5b2, #5fbebb, #71c7c5, #81d0ce);"
            elevation="12"
            max-width="700"
          >
            <v-card-title class="justify-center display-2 font-weight-light pt-5">
              {{ item.title }}
            </v-card-title>
            <v-card-subtitle class="pb-0">
              <v-row>
                <v-col
                  cols="12"
                  md="6"
                >
                  <v-switch
                    v-model="item.column.value"
                    class="mx-2"
                    :label="item.column.name"
                    :value="item.column.value"
                    color="black"
                    dense
                    @change="selectColumn($event, i, item)"
                  />
                </v-col>
                <v-col
                  cols="12"
                  md="6"
                >
                  <v-switch
                    v-model="item.color.value"
                    class="mx-2"
                    :label="item.color.name"
                    :value="item.color.value"
                    color="black"
                    dense
                    @change="selectColor($event, i, item)"
                  />
                </v-col>
              </v-row>
              <v-divider style="margin-bottom: 10px;" />
            </v-card-subtitle>

            <v-card-text>
              <v-item-group
                style="max-height: 150px"
                class="overflow-y-auto"
              >
                <v-list-item
                  v-for="(datos, pos) in item.body"
                  :key="datos.name"
                >
                  <v-list-item-content
                    class="padding-list"
                  >
                    <v-row
                      justify="space-around"
                      align="center"
                    >
                      <v-col
                        cols="12"
                        md="10"
                      >
                        <v-switch
                          v-model="datos.value"
                          class="mx-2 margin-checkbox"
                          :label="datos.name"
                          :value="datos.value"
                          color="black"
                          dense
                          @change="selectList(i, datos, pos, $event)"
                        />
                      </v-col>
                      <v-col
                        cols="12"
                        md="2"
                      >
                        <v-card
                          v-if="item.color.value"
                          class="card-color"
                          :color="datos.color"
                        />
                      </v-col>
                    </v-row>
                  </v-list-item-content>
                </v-list-item>
              </v-item-group>
            </v-card-text>
          </v-card>
        </v-col>
      </v-col>
      <v-col
        cols="12"
        md="9"
        class="no-padding"
      >
        <v-card
          v-if="(entryFinal.length > 0 && changeSelect.length > 0)"
          class="v-card--wizard no-margin is-selected"
          elevation="0"
          color="transparent"
        >
          <v-container
            id="group"
            class="padding-container-principal pa-0"
            fluid
          >
            <v-row>
              <v-col
                v-for="(group, index) in entryFinal"
                :key="index"
                cols="12"
                md="4"
              >
                <v-card
                  id="card-list"
                  :class="group.group ? 'v-card--wizard no-margin pa-0 card-list overflow-y-auto is-select': 'v-card--wizard no-margin pa-0'"
                  elevation="4"
                  color="#F2F2F2"
                  :style="group.group ? 'background-image: linear-gradient(to right top, #81d0ce, #71c7c5, #5fbebb, #4db5b2, #37aca9, #37aca9, #37aca9, #37aca9, #4db5b2, #5fbebb, #71c7c5, #81d0ce);' : ''"
                >
                  <v-card-title
                    v-if="group.group"
                    class="justify-center display-2 font-weight-light pt-5"
                  >
                    {{ group.group }}
                  </v-card-title>

                  <!--  -->
                  <v-dialog
                    v-else
                    v-model="dialog[index]"
                    width="450"
                  >
                    <template v-slot:activator="{ on }">
                      <v-card
                        class="v-card--wizard no-margin justify-center add-padding-cards item-card pointer"
                        elevation="4"
                        :color="(group.color ? group.color : '#F2F2F2')"
                        v-on="on"
                      >
                        <v-card-text class="display-1 pt-5">
                          <p class="justify-center text-h5 font-weight-medium">
                            {{ 'Ticket Nro: ' + group.TicketID }}
                          </p>
                          <p class="justify-center text-body-1">
                            {{ 'Prioridad: ' + group.priority }}
                          </p>
                          <p class="justify-center text-body-1">
                            {{ 'Company: ' + group.customerCompany }}
                          </p>
                        </v-card-text>
                      </v-card>
                    </template>
                    <v-card>
                      <v-toolbar
                        :color="(group.color ? group.color : 'linear-gradient(to right top, #81d0ce, #71c7c5, #5fbebb, #4db5b2, #37aca9, #37aca9, #37aca9, #37aca9, #4db5b2, #5fbebb, #71c7c5, #81d0ce)')"
                        dark
                      >
                        <v-toolbar-title
                          class="headline lighten-2"
                        >
                          {{ 'Info' }}
                        </v-toolbar-title>
                      </v-toolbar>

                      <v-card-text
                        class="justify-center overflow-y-auto"
                        style="max-height: 350px;"
                      >
                        <p
                          v-for="(item, i) in titles"
                          :key="i"
                          class="text-justify"
                        >
                          {{ (group[item] ? item + ': ' + group[item] : item + ': ') }}
                        </p>
                      </v-card-text>
                    </v-card>
                  </v-dialog>
                  <!-- else -->
                  <v-card-text
                    v-if="group.group"
                  >
                    <v-container
                      id="text"
                      class="padding-container card-list"
                      fluid
                    >
                      <v-row>
                        <v-col
                          v-for="(item, ind) in group.body"
                          :key="ind"
                          cols="12"
                          md="6"
                          class="padding-column"
                        >
                          <v-dialog
                            v-model="dialog[index]"
                            width="450"
                          >
                            <template v-slot:activator="{ on }">
                              <v-card
                                class="v-card--wizard no-margin justify-center add-padding-cards item pointer"
                                :color="(item.color ? item.color : 'white')"
                                elevation="2"
                                v-on="on"
                              >
                                <v-card-text class="display-1 pt-5">
                                  <p class="justify-center subtitle-2 font-weight-medium">
                                    {{ 'Ticket Nro: ' + item.TicketID }}
                                  </p>
                                  <!-- <p class="justify-center text-body-2">
                                    {{ 'Prioridad: ' + item.priority }}
                                  </p>
                                  <p class="justify-center text-body-2">
                                    {{ 'Company: ' + item.customerCompany }}
                                  </p> -->
                                </v-card-text>
                              </v-card>
                            </template>
                            <v-card>
                              <v-toolbar
                                :color="(item.color ? item.color : '#F2F2F2')"
                                dark
                              >
                                <v-toolbar-title
                                  class="headline lighten-2"
                                >
                                  {{ 'Info' }}
                                </v-toolbar-title>
                              </v-toolbar>

                              <v-card-text
                                class="justify-center overflow-y-auto"
                                style="max-height: 350px;"
                              >
                                <p
                                  v-for="(itemAux, i) in titles"
                                  :key="i"
                                  class="text-justify"
                                >
                                  {{ (item[itemAux] ? itemAux + ': ' + item[itemAux] : itemAux + ': ') }}
                                </p>
                              </v-card-text>
                            </v-card>
                          </v-dialog>
                        </v-col>
                      </v-row>
                    </v-container>
                  </v-card-text>
                </v-card>
              </v-col>
            </v-row>
          </v-container>
        </v-card>
      </v-col>
    </v-row>
    <!-- </v-container>
  <v-container
    v-else
    id="error"
    fluid
    tag="section"
  >
    <v-card
      class="v-card--wizard no-margin justify-center add-padding-cards"
      elevation="12"
      color="#F2F2F2"
    >
      <v-card-title
        class="justify-center display-2 font-weight-light pt-5"
      >
        {{ 'Esperando datos' }}
      </v-card-title>
    </v-card>
  </v-container> -->
  </v-container>
</template>

<script>
  import _ from 'lodash'
  // import axios from 'axios'

  export default {
    name: 'DashboardDashboard',

    data () {
      return {
        expand: true,
        filterItems: [],
        selectFilter: [],
        mapTitles: [],
        titles: [],
        changeSelect: [],
        body: [],
        entryFinal: [],
        resp_data: [],
        entry: [],
        valid: true,
        sortList: null,
      }
    },
    computed: {
      dialog () {
        return new Array(this.entryFinal.length)
      },
    },
    watch: {
      filterItems (a, b) {
        var arr = this.entry.value
        // console.log('arr', arr)
        this.selectFilter = []
        this.body = []
        var data = []
        // var entry = []
        this.entryFinal = []
        const titlesAux = this.titles

        a.map(function (x) {
          var body = []
          arr.forEach((key, i) => {
            // init color
            const hBase = Math.random()
            const newL = (Math.floor(Math.random() * 16) + 75) * 0.01
            var r, g, b
            const rd = (a) => {
              return Math.floor(Math.max(Math.min(a * 256, 255), 0))
            }
            const hueToRGB = (m, n, o) => {
              if (o < 0) o += 1
              if (o > 1) o -= 1
              if (o < 1 / 6) return m + (n - m) * 6 * o
              if (o < 1 / 2) return n
              if (o < 2 / 3) return m + (n - m) * (4 - o * 6)
              return m
            }
            const q = newL < 0.5 ? newL * 2 : 1
            const p = 2 * newL - q
            r = hueToRGB(p, q, hBase + (1 / 3))
            g = hueToRGB(p, q, hBase)
            b = hueToRGB(p, q, hBase - (1 / 3))
            var c = `#${rd(r).toString(16)}${rd(g).toString(16)}${rd(b).toString(16)}`
            const result = titlesAux.filter(element => element === x.title)
            if (result.length > 0) {
              const valid = body.filter(e => (e.name === key[result[0]]))
              if (key[result[0]] !== undefined) {
                if (!isNaN(key[result[0]])) {
                  if (valid.length === 0) {
                    body.push({
                      name: key[result[0]],
                      value: null,
                      color: c,
                    })
                  }
                } else if (valid.length === 0 && (key[result[0]]).trim() !== '') {
                  body.push({
                    name: key[result[0]],
                    value: null,
                    color: c,
                  })
                }
              }
              // var salario = Object.keys(key[result])
              // if (salario[1] === '#text') {
              //   var money = key.content['m:properties'][result]
              //   const valid = body.filter(e => e.name === money['#text'])
              //   if (valid.length === 0) {
              //     body.push({
              //       name: money['#text'],
              //       value: null,
              //       color: c,
              //     })
              //   }
              // } else {
              //   const validName = body.filter(e => e.name === key.content['m:properties'][result])
              //   if (validName.length === 0) {
              //     body.push({
              //       name: key.content['m:properties'][result],
              //       value: null,
              //       color: c,
              //     })
              //   }
              // }
            }
          })
          data.push({
            title: x.title,
            column: {
              name: 'Columna',
              value: null,
            },
            color: {
              name: 'Color',
              value: null,
            },
            body: body,
          })
        })

        // const removeItems = ['PartitionKey', 'RowKey', 'Timestamp']
        // arr.forEach((key, i) => {
        //   var data = Object.keys(key.content['m:properties'])
        //   var salida = {}
        //   for (let index = 0; index < data.length; index++) {
        //     this.titles.forEach((element, e) => {
        //       salida[element.title] = key.content['m:properties']['d:' + element.title]
        //     })
        //   }
        //   salida = this.formatObj(salida, removeItems)
        //   entry.push(salida)
        //  })

        // entry.map(function (params) {
        //   params = Object.assign(params, { color: null })
        //   // eslint-disable-next-line dot-notation
        //   if (params['Salario']) {
        //     // eslint-disable-next-line dot-notation
        //     params['Salario'] = params['Salario']['#text']
        //   }
        // })
        this.body = arr
        this.selectFilter = data
        this.changeSelect = []
        console.log('body', this.body)
        console.log('selectFilter', this.selectFilter)
      },
    },
    async mounted () {
      console.log('mounted')
      this.entry = require('../../data/data.json')
      this.removeFields(this.entry.value)
      this.headersTitle()
      // console.log('data', this.entry)
      // console.log('titles', this.titles)

      // try {
      // const respData = await axios.get('https://pivottableview.blob.core.windows.net/muck/getticket.json')
      // const baseUrl = 'https://pivottableview.blob.core.windows.net/muck/getticket.json'
      // const axiosConfig = {
      //   crossdomain: true,
      // headers: {
      //   'Access-Control-Allow-Origin': '*',
      //   'Access-Control-Allow-Headers': 'Content-Type',
      //   Accept: 'application/json',
      //   'Content-Type': 'application/json',
      // },
      // }
      // const userAction = async () => {
      //   const response = await fetch('https://pivottableview.blob.core.windows.net/muck/getticket.json')
      //   const myJson = await response.json()
      //   console.log('myJson', myJson)
      // }
      var miInit = {
        method: 'GET',
        headers: {
          'Access-Control-Allow-Origin': '*',
          'Access-Control-Allow-Headers': 'Content-Type',
          Accept: 'application/json',
          'Accept-Encoding': 'identity',
          'Content-Type': 'application/json',
        },
        mode: 'cors',
        cache: 'default',
      }
      const userAction = fetch('https://pivottableview.blob.core.windows.net/muck/getticket.json', miInit).then((resp) => resp.json())
        .then(function (data) {
          console.log(data)
        })
        .catch(function (error) {
          console.log(error)
        })
      // const respData = axios.get(baseUrl, axiosConfig)
      //   .then(response => {
      //     console.log('response----->', response)
      //   })
      //   .catch(error => {
      //     console.log('error----->', error)
      //   })
      console.log('respData', userAction)
      // this.resp_data = respData.data.data.entry
      // this.entry = respData.data.data.entry
      this.valid = true
      // } catch (error) {
      //   console.error(error)
      //   this.valid = false
      // }
      // this.headersTitle()
    },
    beforeUpdate () {
      // this.animationUnselect()
    },
    updated () {
      this.animationSelect()
    },
    methods: {

      removeFields (objects) {
        objects.forEach(element => {
          const propeties = Object.keys(element)
          propeties.forEach((item, i) => {
            if (item.includes('@') || item.includes('.')) {
              delete element[item]
            } else if (!this.titles.includes(item)) this.titles.push(item)
          })
        })
      },

      // -- Metodos para consumir el endpoint
      // async loadData () {
      //   try {
      //     const respData = await axios.get(this.URL, {
      //       headers: {
      //         'Access-Control-Allow-Origin': '*',
      //         'Access-Control-Allow-Methods': 'GET,PUT,POST,DELETE,PATCH,OPTIONS',
      //         'Content-Type': 'application/json',
      //       },
      //       mode: 'no-cors',
      //     })
      //     console.error('respData', respData)
      //   } catch (error) {
      //     console.error(error)
      //   }
      // },

      // loadTest () {
      //   var miInit = {
      //     method: 'GET',
      //     headers: {
      //       'Access-Control-Allow-Origin': '*',
      //       'Access-Control-Allow-Headers': 'Content-Type',
      //       Accept: 'application/json',
      //       'Accept-Encoding': 'identity',
      //       'Content-Type': 'application/json',
      //     },
      //     mode: 'no-cors',
      //     cache: 'default',
      //   }
      //   const userAction = fetch(this.URL, miInit).then((resp) => resp.json())
      //     .then(function (data) {
      //       console.log('data', data)
      //     })
      //     .catch(function (error) {
      //       console.log('error', error)
      //     })
      //   console.log('respData', userAction)
      // },

      // ----

      headersTitle () {
        this.mapTitles = this.titles.map(element => {
          return {
            title: element,
            value: false,
          }
        })
      },
      otherRandomColor () {
        const a = '#' + ('00000' + (Math.random() * (1 << 24) | 0).toString(16)).slice(-6)
        return a
      },
      selectColumn (value, index, event) {
        const arraySelectFilter = this.selectFilter
        if (value === true) {
          this.changeSelect.push({ position: index, name: event.column.name, list: [] })
          event.color.value = null
          const change = this.changeSelect.filter(element => (element.name !== event.column.name) && (element.position === index))
          if (change.length > 0) {
            if (change[0].position === index) {
              this.deltingPosition(index)
            }
          }
          this.distringFilter(index, event, 'column')
          const share = (element) => element.position === index
          var i = this.changeSelect.findIndex(share)
          this.changeSelect[i].list = []
          this.body.forEach(e => { e.color = null })
          this.changeSelect.forEach(val => {
            arraySelectFilter.forEach((params, i) => {
              params.body.forEach((e, position) => {
                if ((val.name === 'Columna') && (e.value === true)) val.list.push({ position: position, name: e.name })
              })
            })
          })
        } else {
          this.deltingPosition(index)
        }
        this.updateArray(this.changeSelect, arraySelectFilter)
      },

      distringFilter: function (i, e, value) {
        const arraySelectFilter = this.selectFilter
        const existDisting = this.changeSelect.filter(element => {
          if (value === 'column') return (element.name === e.column.name) && (element.position !== i)
          else return (element.name === e.color.name) && (element.position !== i)
        })
        if (existDisting.length > 0) {
          if (existDisting[0].position !== i) {
            const exits = (element) => element.position === existDisting[0].position
            var whatIs = this.changeSelect.findIndex(exits)
            this.changeSelect.splice(whatIs, 1)
            this.changeSelect.forEach(function (val) {
              for (let a = 0; a < arraySelectFilter.length; a++) {
                if (value === 'column') {
                  if ((arraySelectFilter[a].column.name === val.name) && (a !== i)) arraySelectFilter[a].column.value = null
                } else {
                  if ((arraySelectFilter[a].color.name === val.name) && (a !== i)) arraySelectFilter[a].color.value = null
                }
              }
            })
          }
        }
      },
      selectColor (value, index, event) {
        const arraySelectFilter = this.selectFilter
        if (value === true) {
          this.changeSelect.push({ position: index, name: event.color.name, list: [] })
          event.column.value = null
          var exist = this.changeSelect.filter(element => (element.name !== event.color.name) && (element.position === index))
          if (exist.length > 0) {
            if (exist[0].position === index) this.deltingPosition(index)
          }
          this.distringFilter(index, event, 'color')
          const share = (element) => element.position === index
          var i = this.changeSelect.findIndex(share)
          this.changeSelect[i].list = []
          event.body.forEach(ckeck => { ckeck.value = true })
          this.changeSelect.forEach(val => {
            arraySelectFilter.forEach((params, i) => {
              params.body.forEach((e, position) => {
                if ((val.name === 'Color') && (e.value === true)) val.list.push({ position: position, name: e.name, color: e.color })
              })
            })
          })
        } else {
          event.body.forEach(ckeck => { ckeck.value = null })
          this.deltingPosition(index)
          this.body.forEach(e => { e.color = null })
        }
        this.updateArray(this.changeSelect, arraySelectFilter)
      },
      selectList (i, data, col, event) {
        if (event === true) {
          this.changeSelect.forEach(function (e) {
            if ((i === e.position) && (e.name === 'Columna')) e.list.push({ position: col, name: data.name })
            if ((i === e.position) && (e.name === 'Color')) e.list.push({ position: col, name: data.name, color: data.color })
          })
        } else {
          const delting = (element) => element.name === data.name
          this.changeSelect.forEach(function (e) {
            if (i === e.position && e.name === 'Columna') {
              var ind = e.list.findIndex(delting)
              e.list.splice(ind, 1)
            }
            if (i === e.position && e.name === 'Color') {
              var indx = e.list.findIndex(delting)
              e.list.splice(indx, 1)
            }
          })
        }
        this.updateArray(this.changeSelect, this.selectFilter)
      },
      formatObj (obj, removeItems) {
        return {
          ...Object.keys(obj)
            .filter(item => !this.isInArray(item, removeItems))
            .reduce((newObj, item) => {
              return {
                ...newObj, [item]: obj[item],
              }
          }, {}),
        }
      },
      isInArray (value, array) {
        return array.indexOf(value) > -1
      },
      updateArray: function (listSelect, listFilter) {
        var body = this.body
        var entryFinal = []
        var auxBody = []

        listSelect.forEach(function (e) {
          listFilter.forEach(function (a) {
            var nameColor = a.title
            if ((e.name === 'Color') && (a.color.value === true)) {
              a.body.forEach(function (x) {
                body.forEach(function (o) {
                  if ((x.name === o[nameColor]) && (x.value === true)) { o.color = x.color }
                  if ((x.name === o[nameColor]) && (x.value === null)) { o.color = null }
                })
              })
              auxBody = body.filter(e => e.color !== null)
              body = auxBody
            }
          })
        })
        listSelect.forEach(function (e) {
          listFilter.forEach(function (a) {
            var nameColumn = a.title
            if ((e.name === 'Columna') && (a.column.value === true)) {
              var result = []
              e.list.forEach(function (i, pos) {
                body.forEach(function (o) {
                  if (o[nameColumn] === i.name) {
                    result.push(o)
                  }
                })
              })
              entryFinal = _.chain(result).groupBy(a.title).map((value, key) => ({ group: key, body: value })).value()
            }
          })
        })

        if (entryFinal.length === 0) {
          this.entryFinal = []
          this.animationUnselect()
          this.entryFinal = this.sortColor(body)
        } else {
          entryFinal.forEach(aux => {
            aux.body = this.sortColor(aux.body)
          })
          this.entryFinal = entryFinal
        }
        console.log('entryFinal', this.entryFinal)
      },
      sortColor (array) {
        return array.sort((a, b) => {
          if (a.color < b.color) {
            return -1
          }
          if (a.color > b.color) {
            return 1
          }
          return 0
        })
      },
      deltingPosition (i) {
        const delting = (element) => element.position === i
        var indexDelete = this.changeSelect.findIndex(delting)
        this.changeSelect.splice(indexDelete, 1)
      },
      animationSelect () {
        this.sortList = document.getElementsByClassName('card-list')
        if (this.sortList.length) {
          console.log('animationSelect', this.sortList)
          for (var i = 0; i < this.sortList.length; i++) {
            this.sortList[i].classList.add('is-selected')
          }
        }
      },
      animationUnselect () {
        this.sortList = document.getElementsByClassName('card-list')
        if (this.sortList.length) {
          console.log('animationUnselect', this.sortList)
          for (var i = 0; i < this.sortList.length; i++) {
            this.sortList[i].classList.remove('is-selected')
            this.sortList[i].classList.add('.item')
          }
        }
      },
    },
  }
</script>
<style lang="scss" scoped>
@import "../../assets/style.scss";
</style>
