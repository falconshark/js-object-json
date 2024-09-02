<template>
  <main>
    <div class="main-content">
      <div class="container">
        <div class="title">
          Object to JSON tool 
        </div>
        <div class="description">
          A tool for convert Javascript object to JSON
        </div>
        <div class="input-form">
          <div class="form-group">
            <label>Javascript Code</label>
            <textarea class="form-control" id="code" rows="10" v-model="code"></textarea>
          </div>
          <div class="generate-button-wrapper">
            <button class="btn btn-primary generate-button" @click="convertToJson">
              Generate!
            </button>
          </div>
          <div class="generate-result">
            <label>Result</label>
            <textarea class="form-control" id="result" rows="10" v-model="result"></textarea>
          </div>
        </div>
      </div>
    </div>
  </main>
</template>

<script>
import JSON5 from 'json5';
export default {
  name: 'App',
  data() {
    return {
      code: '',
      result: '',
    }
  },
  methods: {
    convertToJson() {
      try {
        let code = this.code;
        const formatRegax = new RegExp('([a-zA-Z]+)(\:)', 'g');
        //Check the object string's key is missing "". If it is missed, add it back.
       if(code.match(formatRegax)){
         code = code.replace(/([a-zA-Z]+)(\:)/g, '"$1":');
        }
        //Replace unnecessary part from javascript object
        code = code.replace(/(\r\n|\n|\r)/gm, "");
        code = code.replace(/\}\;/g, "}");
        code = JSON.stringify(JSON5.parse(code));
        this.result = code;
      } catch (ex) {
        console.log(ex);
      }
    },
  }
}
</script>

<style lang="scss">
.title {
  font-size: 3em;
  font-weight: bold;
  text-align: center;
  margin-top: 50px;
  margin-bottom: 10px;
}

.description {
  font-size: 2em;
  text-align: center;
  margin-bottom: 5px;
}

.generate-button-wrapper{
  text-align: center;
  margin-bottom: 20px;
}
.form-group{
  margin-bottom: 20px;
}
label{
    margin-bottom: 10px;
    font-size: 1.2em;
    font-weight: bold;
}
.generate-result{
  margin-bottom: 20px;
}
  
</style>
