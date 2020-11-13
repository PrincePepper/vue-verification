<template>
  <div>
    <form novalidate @submit.prevent="userRegister">
      <div class="input-group mb-3">
        <b-input-group class="mb-2" prepend="Имя и Фамилия">
          <b-form-input v-model="formReg.name"
                        :class="{'is-invalid': $v.formReg.name.$error}"
                        aria-label="First name" type="text"
                        @blur="$v.formReg.name.$touch()">
          </b-form-input>
          <b-form-input v-model="formReg.surname"
                        :class="{'is-invalid': $v.formReg.surname.$error}"
                        aria-label="Last name" type="text"
                        @blur="$v.formReg.surname.$touch()">
          </b-form-input>
          <div v-if="!$v.formReg.name.required" class="invalid-feedback">{{ reqText }}</div>
          <div v-if="!$v.formReg.name.alpha" class="invalid-feedback">{{ alphaText }}</div>

          <div v-if="!$v.formReg.surname.required" class="invalid-feedback">{{ reqText }}</div>
          <div v-if="!$v.formReg.surname.alpha" class="invalid-feedback">{{ alphaText }}</div>
        </b-input-group>
      </div>
      <div class="form-inline mb-3">
        <div class="form-group year">
          <b-input-group prepend="Возраст">
            <b-form-input v-model="formReg.old"
                          :class="{'is-invalid': $v.formReg.old.$error}"
                          class="year-num"
                          type="number"
                          @blur="$v.formReg.old.$touch()">
            </b-form-input>
            <div v-if="!$v.formReg.old.required" class="invalid-feedback">{{ numberText }}</div>

          </b-input-group>
        </div>
        <div class="form-group">
          <label class="indent" for="exampleFormControlSelect1">Пол</label>
          <select id="exampleFormControlSelect1" class="form-control">
            <option>Мужской👦</option>
            <option>Женский🧔‍</option>
            <option>Единорог&#129412;</option>
          </select>
        </div>
        <div class="form-group indent">
          <b-input-group prepend="Год рождения">
            <b-form-input
                id="year"
                v-model="formReg.year"
                :class="{'is-invalid': $v.formReg.year.$error}"
                type="date"
                @blur="$v.formReg.year.$touch()">
            </b-form-input>
            <div v-if="!$v.formReg.year.required" class="invalid-feedback">{{ reqText }}</div>
          </b-input-group>
        </div>
      </div>
      <div class="form-group">
        <b-input
            v-model="formReg.telephone"
            :class="{'is-invalid': $v.formReg.telephone.$error}"
            placeholder="Номер телефона"
            type="number"
            @blur="$v.formReg.telephone.$touch()"/>
        <div v-if="!$v.formReg.telephone.required" class="invalid-feedback">{{ reqText }}</div>
        <br>
        <b-textarea v-model="formReg.textarea"
                    :class="{'is-invalid': $v.formReg.textarea.$error}"
                    placeholder="О себе" type="text"
                    @blur="$v.formReg.textarea.$touch()"></b-textarea>
        <div v-if="!$v.formReg.textarea.required" class="invalid-feedback">{{ reqText }}</div>
      </div>
      <div class="form-group mb-5">
        <label>Напишите на каких языках программирования ты пишешь</label>
        <b-form-tags
            v-model="value"
            :input-attrs="{ 'aria-describedby': 'tags-remove-on-delete-help' }"
            input-id="tags-remove-on-delete"
            placeholder="пиши сюда языки"
            remove-on-delete
            separator=" "/>
        <b-form-text id="tags-remove-on-delete-help" class="mt-2 text-left">
          Нажми <kbd>Backspace</kbd> чтобы удалить
        </b-form-text>
      </div>

      <button :disabled="disabledBtn" class="btn btn-primary" type="submit">Зарегистрироваться</button>
    </form>

  </div>

</template>

<script>
import {between, decimal, email, helpers, required} from 'vuelidate/lib/validators'

const alpha = helpers.regex('alpha', /^[a-zA-Zа-яёА-ЯЁ]*$/)
export default {
  data() {
    return {
      value: ['Trololo', 'C#', 'Assembler'],
      regMessage: false,
      reqText: 'Поле обязательно для заполнения',
      alphaText: 'Запрещены цифры, пробелы и другие символы',
      numberText: 'Только положительное число',
      minLengthText: 'Минимальная длина 6 символов!',
      passwordConfirmText: 'Пароли не совпадают',
      formReg: {
        name: '',
        surname: '',
        year: '',
        old: '',
        telephone: '',
        textarea: ''
      }
    }
  },
  computed: {
    disabledBtn() {
      return this.$v.formReg.name.$invalid ||
          this.$v.formReg.surname.$invalid ||
          this.$v.formReg.year.$invalid ||
          this.$v.formReg.old.$invalid ||
          this.$v.formReg.telephone.$invalid ||
          this.$v.formReg.textarea.$invalid;
    }
  },
  methods: {
    userRegister() {
      console.group("Form first")
      console.log('Вы успешно зарегистрированны!')
      console.log('Ваше имя: ' + this.formReg.name)
      console.log('Ваша фамилия: ' + this.formReg.surname)
      console.log('Год рождения: ' + this.formReg.year)
      console.log('Возвраст: ' + this.formReg.old)
      console.log('Телефон: ' + this.formReg.telephone)
      console.groupEnd()
      this.reset()

    },
    reset() {
      for (let input in this.formReg) {
        this.formReg[input] = ''
      }
      // сбросить валидацию
      this.$v.$reset()
    }
  },
  validations: {
    formReg: {
      email: {
        email,
        required
      },
      name: {
        required,
        alpha
      },
      surname: {
        required,
        alpha
      },
      year: {
        required
      },
      old: {
        required,
        decimal,
        between: between(18, 35)
      },
      telephone: {
        required,
        decimal
      },
      textarea: {
        required
      }
    }
  },

}
</script>

<style scoped>

.year {
  width: 25%;
}

.year-num {
  text-align: center;
}

.indent {
  margin-left: 10px;
  margin-right: 5px;
}

.is-invalid {
  border-color: #ff8300 !important;
  box-shadow: 0 0 0 0.2rem rgba(255, 131, 0, 0.30) !important;
  color: #ff8300 !important;
  background-image: url("data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' width='12' height='12' fill='none' stroke='%23ff8300' viewBox='0 0 12 12'><circle cx='6' cy='6' r='4.5'/><path stroke-linejoin='round' d='M5.8 3.6h.4L6 6.5z'/><circle cx='6' cy='8.2' r='.6' fill='%23ff8300' stroke='none'/></svg>") !important;
}

.invalid-feedback {
  color: #ff8300 !important;
}

form {
  background-color: white;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 10px 10px 45px -31px rgba(0, 0, 0, 0.75);
}

</style>
