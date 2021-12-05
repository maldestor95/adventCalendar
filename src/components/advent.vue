<template>
    <div >
        <section class="main-img">
            <!-- <img :src="getimgpath('main')" class="main-img" alt=""/> -->

          <div class="year">{{imgpath.split('/')[0]}}</div>
          <div class="wrapper">
            <div v-for="item in days" class="day"
              :key="item.id"
              @click="currentimg=item;openmodal(item)"
            >
            {{ item }}
            </div>
          </div>

        </section>

        <div class="modal" :style="{display:displaymodal}">
          <div class="modal-content">
            <img :src="getimgpath(currentimg)" alt="" >
            <v-icon class="white--text topleft " @click="closemodal()">mdi-close</v-icon>
          </div>
        </div>
    </div>
</template>

<script>
export default {
  props: {
    imgpath: {
      type: String,
      default: () => '2021/fr',
    },
  },
  data() {
    return {
      key: 0,
      currentimg: '',
      days: [
        2,
        14,
        4,
        6,
        21,
        8,
        7,
        22,
        5,
        10,
        16,
        24,
        11,
        12,
        9,
        13,
        23,
        15,
        1,
        17,
        18,
        3,
        19,
        20,

      ],
      displaymodal: 'none',

    };
  },
  methods: {
    getimgpath(imgname) {
      const year = this.imgpath.split('/')[0];
      const calendardate = new Date(year, 11, imgname);
      let imgToDisplay = imgname;
      if (imgToDisplay === '') return '';
      if (new Date().getDate() < calendardate.getDate()) imgToDisplay = 'tooearly';

      return `https://maldestor95.github.io/adventpics/${this.imgpath}/${imgToDisplay}.jpg`;
    },
    openmodal() {
      this.displaymodal = 'block';
    },
    closemodal() {
      this.currentimg = '';
      this.displaymodal = 'none';
    },
  },

};
</script>

<style lang="scss" scoped>
$imgradius:8px;
.modal {
  display: none; /* Hidden by default */
  position: fixed; /* Stay in place */
  z-index: 1; /* Sit on top */
  left: 0;
  top: 0;
  width: 100%; /* Full width */
  height: 100%; /* Full height */
  overflow: auto; /* Enable scroll if needed */

  background-color: rgb(0,0,0); /* Fallback color */
  background-color: rgba(0,0,0,0.4); /* Black w/ opacity */
}
.main-img {
    // width: 100%;
    // object-fit: scale-down;
    // background-repeat: repeat;
    background-image:
    linear-gradient(to bottom, rgba(255,255,0,0.5), rgba(0,0,255,0.5))
}
.modal-content {
  background-color: #fefefe;
  position:absolute;
  top:3rem;
  // left:10%;
  max-width: 80%;
  padding: 20px;
  border: 0px solid #888;
  border-radius: $imgradius;
}
.topleft {
  position:absolute !important;
    top:0px;
    left: 0px;
    width: 20px;
    background: red !important;
    border-radius: $imgradius 0 $imgradius 0;
}
.modal-content > img {
  max-width: 100%;
  object-fit: scale-down;
  border-radius: $imgradius;
}

.widowframe {
    position: absolute;
    border: 5px dashed white;
    color:white;
    font-size: 5rem;
    margin: auto;
    padding: auto;
    text-align: center;
}

.wrapper {
  display: flex;
  width: 100%;
  flex-wrap: wrap;
  justify-content: space-evenly;

}
.year {

  width: 100%;
  font-size: 5rem;
  text-align: center;
}
.day {
  border: 2px dashed green;
  border-radius: 0.5rem;
    color:green;
    font-size: 1.5rem;
    min-width: 25%;
    margin: 0.2rem;
  // align-content: stretch;
  text-align: center;
}
@media screen and (min-width: 640px){
  .day {
    margin: 1.2rem;
    font-size: 5rem;
    min-width: 10rem;
  }

  .modal-content {
    display: block;
    text-align: end;
    ;
}
  .modal-content > img{
    max-height: 600px;
  }
}

.wrapper :nth-child(2){
  // flex-grow: 2;
  align-self: flex-start;
}
.wrapper :nth-child(3){
  min-height: 10rem;
  flex-grow: 6;
  align-self: flex-start;
}

</style>
