<template>
  <div>
    <!-- nav -->
    <b-container>
      <b-row class="vh-100 text-center" style="width=100vw" align-v="center">
        <b-col class="center d-flex justify-content-center">
          <b-row class="" align-v="center" style="width=60vw">
            <b-col class="" style="width:60vw">
              <b-card style="width:60vw;">
                <items />
              </b-card>
            </b-col>
          </b-row>

          <!-- <b-card class=" aligns-items-center bg-dark">
            <b-card-text style=" ">
              Some quick example text to build on the card and make up the bulk
              of the card's content.
            </b-card-text>
          </b-card> -->
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import items from "./items.vue";
export default {
  components: { items },
  name: "container",
  data() {
    return {
      msg: ""
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.center {
  width: 60vw;
  height: 60vh;
  background-image: linear-gradient(rgb(118, 206, 247), rgb(248, 232, 177));

  border-radius: 40px;
}
.center:hover {
  transform: scale(1.2);
  background-image: linear-gradient(rgb(51, 156, 255), rgb(255, 255, 255));
}

.center {
  background-image: linear-gradient(
    to right,
    #1fa2ff 0%,
    #12d8fa 51%,
    #1fa2ff 100%
  );
}
.center {
  margin: 10px;
  padding: 15px 45px;
  text-align: center;
  /* text-transform: uppercase; */
  transition: 0.5s;

  background-size: 200% auto;

  box-shadow: 0 0 20px #eee;
  border-radius: 10px;
  display: block;
}

.center:hover {
  background-position: right center; /* change the direction of the change here */

  text-decoration: none;
}

/*  */
</style>
