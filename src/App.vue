<template>
  <div class="profile">
    <div class="wrap">
      <div class="profile__title">
        <h1 class="title">Профіль лікаря</h1>
      </div>
      <div class="doctor">
        <div class="doctor__block">
          <p class="doctor__block_name">Тестова Оксана Василівна</p>
          <div class="doctor__block_ratting">
            <i class="fa-solid fa-star"></i>
            <i class="fa-solid fa-star"></i>
            <i class="fa-solid fa-star"></i>
          </div>
          <p class="doctor__block_value">(Середня оцінка: 3)</p>
        </div>
        <div class="doctor__desc">
          <div class="doctor__desc_photo">
            <img src="@/assets/images/doctor.png" alt="avatar" />
          </div>
          <div class="doctor__desc_text">
            <div class="doctor__desc_text_left">
              <p class="place">Місто:</p>
              <p class="place">Місце Роботи:</p>
              <p class="place">Заклад:</p>
            </div>
            <div class="doctor__desc_text_right">
              <p class="city">Львів</p>
              <p class="city">Львів, площа Ринок, 10</p>
              <p class="city">
                Відділення надання екстренної допомоги черговим лікарем у <br />
                закладі стаціонарної допомоги імені Пилипіва Юрію
              </p>
            </div>
            <Comments />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Comments from "./components/Comments.vue";

export default {
  name: "App",
  components: {
    Comments,
  },
};
</script>

<style lang="scss">
@import "@/assets/style/main.scss";

.profile {
  border: 2px solid $light-blue;
  padding-bottom: 50px;
  &__title {
    background: $blue;
    padding: 20px 0;
    text-align: center;
    margin-bottom: 20px;
    .title {
      color: $white;
    }
  }
  .doctor {
    max-width: 1000px;
    margin: auto;
    &__block {
      display: flex;
      align-items: center;
      &_name {
        font-size: 22px;
        text-transform: uppercase;
        color: $birch;
      }
      &_ratting {
        margin: 0 15px;
        .fa-star {
          color: $yellow;
        }
      }
    }
    &__desc {
      border: 1px solid $grey;
      padding: 10px;
      display: flex;
      &_photo {
        width: 219px;
        height: 243px;
        margin-left: 20px;
        img {
          width: 100%;
          height: 100%;
        }
      }
      &_text {
        display: flex;
        margin: 20px 0 0 20px;
        &_left {
          margin-right: 30px;
          .place {
            font-weight: 700;
            margin-bottom: 5px;
          }
        }
        &_right {
          .city {
            margin-bottom: 5px;
            &:nth-child(3) {
              color: $blue;
            }
          }
        }
      }
    }
  }
}
</style>
