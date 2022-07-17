<template>
  <div class="container-fluid position-relative flex-column navbar-center search-box" :id="id" :class="width"
       @click="$event.stopPropagation()">
    <input :class="classname" @keyup="input" v-model="term" @click="click" class="input">
    <div class="dropdown" :class="isExists ? 'showing':'hiding'">
      <ul class="dropdown-menu vld-parent" :class="isShow ? 'show':'hiding'">
        <li class="not-found" :style="{'display': notFound ? 'block':'none'}"><a class="dropdown-item text-center">Aradığınız
          Sonuç Bulunamadı!</a></li>
        <li v-for="i in tempArray" class="li" @click="select(i.text)">
          <div class="d-flex dropdown-item">
            <div class="flex-shrink-0">
              <img src="https://via.placeholder.com/150" class="img-thumbnail" alt="Sample Image">
            </div>
            <div class="flex-grow-1 ms-3">
              <a>{{ i.text }} <small class="text-muted"><i>{{ i.price}} </i></small></a>
              <p class="text-wrap">
                {{ 'Lorem ipsum dolor sit amet, consectetur adipisicing elit. A accusantium dolor dolorem doloribus, facilis incidunt ipsa iure iusto minus nobis obcaecati perspiciatis quam qui quidem sunt temporibus tenetur vero voluptatem.' }}</p>
            </div>
          </div>
        </li>
      </ul>
    </div>
    <fa icon="search" id="search-icon"></fa>
  </div>

</template>
<script>

export default {
  updated () {
    document.querySelector('html').addEventListener('click', function (e) {
      const id = this.getId()
      $(`#${id} .dropdown, #${id} .dropdown-menu`).addClass('hiding')
    }.bind(this))
    $('.input').click(function () {
      const id = this.getId()
      $(`#${id} .dropdown, #${id} .dropdown-menu`).removeClass('hiding')
    }.bind(this))
  },
  props: {
    data: Array,
    id: String,
    classname: String,
    width: String
  },
  data () {
    return {
      isShow: false,
      term: '',
      tempArray: [],
      isExists: false,
      notFound: false,
    }
  },
  name: 'autoComplete',
  methods: {
    select (value) {
      this.term = value
      this.isShow = false
    },
    getId () {
      return this.id
    },
    click () {
      if (this.tempArray.length > 0) {
        this.isShow = true
      }
    },
    input () {
      this.isExists = true
      this.tempArray = []
      this.tempArray = this.data.filter(function (i, k) {
        return i.text.indexOf(this.term.toString().toLowerCase()) > -1
      }.bind(this))

      if (this.tempArray.length) {
        this.notFound = false
        this.isShow = true
      } else {
        this.onNotFound()
      }
    },
    onNotFound () {
      this.isShow = true
      this.notFound = true
    }
  }
}
</script>
<style>
.li {
  border-bottom: 1px solid lightgray;
}

.dropdown-menu li:last-child {
  border: none;
}

.dropdown-menu {
  width: 100%;
  overflow-y: auto;
  max-height: 400px;
}

.hiding {
  visibility: hidden;
}

.showing {
  visibility: visible;
}

.img-thumbnail {
  max-height: 75px;
}

#search-icon {
  position: absolute;
  right: 20px;
  top: 10px;
  font-size: 20px;
}

</style>
