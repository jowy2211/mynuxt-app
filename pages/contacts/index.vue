<template>
  <div>
    <div class="contacts-layout">
      <div class="contacts-header">
        <h2>My list contact</h2>
      </div>
      <div class="contacts-main">
        <div class="render-list">
          <ul v-for="item in listContacts" :key="item.id" class="main-list">
            <li class="item-list">
              <div class="item">
                <div class="image-item">
                  <img :src="item.avatarLink" />
                </div>
                <div class="detail-item">
                  <span>{{ item.firstName + ' ' + item.lastName }}</span>
                  <p>{{ item.profession }}</p>
                </div>
                <div class="info-item">
                  <nuxt-link
                    :to="{ path: '/contacts/see', query: { detail: item.id } }"
                    class="btn btn-md btn-info"
                    >See</nuxt-link
                  >
                  <button class="btn btn-md btn-danger">Delete</button>
                </div>
              </div>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Axios from 'axios'
export default {
  data() {
    return {
      listContacts: []
    }
  },
  mounted() {
    Axios.get('https://maindata.herokuapp.com/users').then(({ data }) => {
      this.listContacts = data.result
      this.listContacts.map((val) => {
        if (val.avatarLink === 'N/A') {
          val.avatarLink =
            'https://semantic-ui.com/images/avatar2/large/kristy.png'
        }
      })
    })
  },
  layout: 'main'
}
</script>
