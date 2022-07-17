<template>
    <autoComplete :data="currentOptions" :id="inputId" :classname="className" :width="width"></autoComplete>
</template>
<script>
import autoComplete from './autocomplete'

export default {
  name: 'searchBox',
  created () {
    this.getPosts()
  },
  components: {
    autoComplete
  },
  props: {},
  methods: {
    getPosts () {
        for (let index = 0; index < array.length; index++) {
            this.currentOptions.push({id:index,text:`Test-${index}`});
        }
  },
  data () {
    return {
      currentOptions: [],
      currentValue: '',
      inputId: 'search',
      className: 'form-control',
      width: 'w-50',
      // loader:false
    }
  }
}
</script>
<style>
@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/5.15.4/css/all.min.css');

form {
  margin: 0 auto;
}

form span {
  width: 100%;
}

.infinite-autocomplete-wrapper input {
  height: 45px !important;
  width: 100%;
  text-indent: 3px;
  border-radius: unset !important;
}

.infinite-autocomplete-wrapper ul {
  width: 100%;
  overflow-y: auto !important;
  max-height: 400px !important;
}

.infinite-autocomplete-wrapper ul li {
  border-bottom: 1px solid lightgray;
}

.infinite-autocomplete-wrapper ul li:last-child {
  border: unset;
}

.infinite-autocomplete-wrapper input {
  display: block;
  width: 100%;
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  font-weight: 400;
  line-height: 1.5;
  color: #212529;
  background-color: #f7f9fb;
  background-clip: padding-box;
  border: 1px solid #ced4da;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  border-radius: 0.125rem;
  transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
}

.infinite-autocomplete-wrapper input:focus {
  border-color: rgba(126, 239, 104, 0.8);
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.075) inset, 0 0 8px rgba(126, 239, 104, 0.6);
  outline: 0 none;
}

.search-icon {
  position: absolute;
  right: 10px;
  top: 13px;
  font-size: 19px;
}
</style>
