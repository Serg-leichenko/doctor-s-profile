<template name="modal-comments">
  <div class="modal">
    <div class="modal-border">
      <div class="modal__title">
        <p class="title">Залишити оцінку та відгук</p>
      </div>
      <form class="modal__fields">
        <div class="modal__fields_left">
          <p class="text">Представтесь:<sup class="red-star">*</sup></p>
          <p class="text">
            Оцініть роботу лікаря:<sup class="red-star">*</sup>
          </p>
          <p class="text">Напишіть відгук:<sup class="red-star">*</sup></p>
        </div>
        <div class="modal__fields_right">
          <div class="modal__fields_right_name">
            <input
              type="text"
              placeholder="Вкажіть ваше прізвище та ім'я"
              class="fild-name"
              :maxlength="limitName"
              v-model="form.name"
              :disabled="disabled"
              :class="{ disabled: disabled }"
            />
            <div class="anonim">
              <input
                type="checkbox"
                id="anonim"
                name="anonim"
                class="anonim__check"
                @click="disabled = !disabled"
              />
              <label for="anonim" class="anonim__text">Анонімно</label>
            </div>
          </div>
          <!-- ratting icons -->
          <div class="modal__fields_right_stars">
            <div class="stars-block" @mouseout="mouseOver = null">
              <image-rating
                :src="src"
                v-model="form.ratting"
                :item-size="50"
                :spacing="42"
                :max-rating="5"
                :show-rating="false"
                @current-rating="mouseOver = $event"
              ></image-rating>
              <div class="text-r-block">
                <p
                  class="text-r-block__text"
                  v-for="item in itemRatting"
                  :key="item.id"
                >
                  {{ item.text }}
                </p>
              </div>
            </div>
          </div>
          <!-- end ratting icons -->
          <div class="modal__fields_right_comment">
            <textarea
              rows="10"
              placeholder="Вкажіть відгук до 500 символів"
              class="comments-fild"
              :maxlength="limitText"
              v-model="form.text"
            ></textarea>
          </div>
          <div class="modal__fields_right_buttons">
            <button type="submit" class="btn" @click="clearForm">
              Очистити
            </button>
            <button type="submit" class="btn" @click.prevent="submitForm">
              Надіслати
            </button>
          </div>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
import { ImageRating } from "vue-rate-it";
export default {
  name: "modal-comments",
  components: {
    ImageRating,
  },
  data: () => {
    return {
      mouseOver: null,
      src: require("@/assets/images/star.png"),
      limitName: 50,
      limitText: 500,
      disabled: false,
      form: {
        name: "",
        ratting: 0,
        text: "",
      },
      itemRatting: [
        { id: 1, text: "Дуже погано" },
        { id: 2, text: "Погано" },
        { id: 3, text: "Нормально" },
        { id: 4, text: "Добре" },
        { id: 5, text: "Дуже добре" },
      ],
    };
  },
  methods: {
    submitForm() {
      if (this.disabled === true) {
        const data = {
          ratting: this.form.ratting,
          text: this.form.text,
        };
        console.log("anonim", data);
      } else {
        console.log("all form", this.form);
      }
    },
    clearForm() {
      this.disabled = !this.disabled;
      this.form.ratting = 0;
      this.form.name = "";
      this.form.text = "";
    },
  },
};
</script>

<style scoped lang="scss">
@import "@/assets/style/main.scss";

.modal {
  background: linear-gradient(to bottom, #2530c169 0%, #14148dc2 100%);
  padding: 2px;
  z-index: 1;
  position: absolute;
  top: 245px;
  .modal-border {
    padding: 20px 20px 10px 30px;
    background: linear-gradient(
      to bottom,
      $white 40%,
      rgb(0 102 255 / 91%) 100%
    );
  }
  &__title {
    color: $blue;
    text-transform: uppercase;
    text-align: center;
    font-size: 16px;
    font-weight: 700;
    margin-bottom: 20px;
  }
  &__fields {
    display: flex;
    justify-content: space-between;
    &_left {
      width: 30%;
      .text {
        color: $blue;
        font-weight: 700;
        margin-top: 40px;
        &:nth-child(1) {
          margin-top: 0;
        }
        .red-star {
          color: $red;
        }
      }
    }
    &_right {
      width: 70%;
      &_name {
        display: flex;
        .fild-name {
          border: 2px solid $dark-grey;
          width: 80%;
          height: 10px;
          padding: 10px;
          outline: none;
          &::placeholder {
            color: $grey;
            text-align: center;
            font-style: italic;
          }
        }
        .disabled {
          border: 2px solid $grey;
        }
        .anonim {
          display: flex;
          flex-direction: column;
          align-items: center;
          margin-top: 5px;
          text-align: center;
          &__check {
            position: absolute;
            opacity: 0;
            & + label {
              position: relative;
              cursor: pointer;
              padding: 0;
              color: $blue;
              font-weight: 700;
            }
            & + label:before {
              content: "";
              display: inline-block;
              vertical-align: text-top;
              width: 20px;
              height: 20px;
              border: 2px solid $dark-grey;
              margin-bottom: 8px;
            }
            &:checked + label:after {
              content: "";
              position: absolute;
              left: 34px;
              top: 11px;
              background: $black;
              width: 2px;
              height: 2px;
              box-shadow: 2px 0 0 $black, 4px 0 0 $black, 4px -2px 0 $black,
                4px -4px 0 $black, 4px -6px 0 $black, 4px -8px 0 $black;
              transform: rotate(45deg);
            }
          }
        }
      }
      &_stars {
        // margin: 10px 0 20px 0;
        .stars-block {
          margin-bottom: 10px;
          display: flex;
          flex-direction: column;
          .text-r-block {
            display: flex;
            &__text {
              cursor: pointer;
              font-size: 12px;
              color: $blue;
              margin-top: 5px;
              &:nth-child(1) {
                margin-left: -12px;
              }
              &:nth-child(2) {
                margin-left: 37px;
              }
              &:nth-child(3) {
                margin-left: 42px;
              }
              &:nth-child(4) {
                margin-left: 38px;
              }
              &:nth-child(5) {
                margin-left: 49px;
              }
            }
          }
        }
      }
      &_comment {
        .comments-fild {
          border: 2px solid $dark-grey;
          width: 95%;
          height: 100px;
          padding: 10px;
          outline: none;
          &::placeholder {
            color: $grey;
            font-style: italic;
          }
        }
      }
      &_buttons {
        display: flex;
        .btn {
          border: 2px solid $dark-grey;
          padding: 10px 30px;
          color: $blue;
          cursor: pointer;
          outline: none;
          font-weight: 700;
          &:nth-child(2) {
            margin-left: 40px;
          }
          &:hover {
            background: $birch;
          }
        }
      }
    }
  }
}
</style>
