<template>
  <v-container class="" style="max-width:1600px">
    <Snakebar
      :message="snakeBarMessage"
      :isShow.sync="isSnakeBarVisible"
      :color="snakeBarColor"
      :timeout="snakeBarTimeOut"
    />
    <v-row class="">
      <v-col>
        <v-toolbar class="elevation-0" style="border:1px solid #e0e0e0;border-radius:5px;">
          <v-toolbar-title class="google-font mr-3">Emails Details:</v-toolbar-title>
          <v-spacer></v-spacer>
          <!-- Mobile -->
          &nbsp;
          <!-- <AddTeam class="ml-2" @showSuccess="showSnakeBar" /> -->
        </v-toolbar>
      </v-col>
    </v-row>

    <v-row class="mx-0">
      <v-container fluid>
        <v-row>
          <v-col md="7" class="elevation-0 px-2 mx-0 " style="border:1px solid #e0e0e0;border-radius:5px;background:white">
            <v-container fluid>
              <v-row>
                <v-col>
                  <v-text-field
                    label="Subject"
                    placeholder="Subject"
                    outlined
                    v-model="mailData.subject"
                  ></v-text-field>
                </v-col>

                <v-col class="my-0 py-0" cols="12">
                  <v-combobox
                    v-model="mailData.emailids"
                    chips
                    clearable
                    label="Email Ids"
                    multiple
                    outlined
                  >
                    <template v-slot:selection="{ attrs, item, select, selected }">
                      <v-chip
                        v-bind="attrs"
                        :input-value="selected"
                        close
                        @click="select"
                        @click:close="remove(item)"
                      >
                        <strong class="google-font">{{ item }}</strong>
                      </v-chip>
                    </template>
                  </v-combobox>
                </v-col>

                <v-col cols="12">
                  <v-text-field
                    label="Image URL"
                    placeholder="Subject"
                    outlined
                    v-model="mailData.image"
                  ></v-text-field>
                </v-col>

                <v-col cols="6">
                  <v-text-field
                    label="Button Name"
                    outlined
                    v-model="mailData.urlname"
                  ></v-text-field>
                </v-col>

                <v-col cols="6">
                  <v-text-field
                    label="Button URL"
                    v-model="mailData.url"
                    outlined
                  ></v-text-field>
                </v-col>

                <v-col cols="12">
                  <v-text-field
                    label="Title"
                    v-model="mailData.title"
                    outlined
                  ></v-text-field>
                </v-col>

                <v-col cols="12">
                  <v-textarea
                    outlined
                    name="input-7-4"
                    label="Body"
                    v-model="mailData.msg"
                  ></v-textarea>
                </v-col>

              </v-row>
            </v-container>
          </v-col>
          <v-col md="5" class="elevation-0 px-2 py-0 mx-0" >
            <v-container class="py-0 px-0" fluid style="border:1px solid #e0e0e0;border-radius:5px;background:white"  >
              <v-row class="py-3" style="background-color:#fafafa"> 
                <v-col class="text-center">
                  <p class="google-font mb-0" style="font-size:150%;">{{generalConfig.name.length?generalConfig.name:'Aura Admin'}}</p>
                </v-col>
              </v-row>
              <v-row class="pa-0 ma-0">
                <v-col class="pa-0 ma-0">
                  <v-img v-if="mailData.image.length>0" class="ma-0 pa-0" width="100%" :src="mailData.image"></v-img>
                </v-col>
              </v-row>
              <v-row class="px-3 py-5">
                <v-col>
                  <p class="googl-font" style="font-size:130%"><b>{{mailData.title}}</b></p>
                  <dev v-html=mailData.msg></dev>   
                </v-col>
              </v-row>
            </v-container>
          </v-col>
        </v-row>
      </v-container>
      
    </v-row>
  </v-container>
</template>

<script>
import { mapState } from 'vuex';
export default {
  name: "ViewEmailView",
  inject: ['theme'],
  components: {
    Snakebar:()=>import('@/components/Common/Snakebar')
  },
  data: () => ({
    snakeBarMessage: "",
    isSnakeBarVisible: false,
    snakeBarColor: "green",
    snakeBarTimeOut: 5000,
    showDialog: false,
    
    mailData:{
      title:'This is Title Field',
      subject:'This is Subject',
      emailids:[],
      msg:'the Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through. the Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.the Woodman set to work at once, and so sharp was his axe that the tree was soon chopped nearly through.',
      urlname:'Learn More',
      url:'https://google.com',
      image:'https://iambharat.tk/images/roadshow.png'
    }
  }),
  computed:{
      ...mapState(['generalConfig']),
  },
  mounted() {
  },
  methods: {
    remove (item) {
      this.mailData.emailids.splice(this.mailData.emailids.indexOf(item), 1)
      this.mailData.emailids = [...this.mailData.emailids]
    },
  }
};
</script>
