<template>
<mainInfoUser>
    <form class="main-form" action="" >
        <div class="form-1" v-show="this.countPage == 1">
            <input type="text" 
            placeholder="Фамилия*" 
            v-model="userFamily"
            >
            <p class="error">{{ error }}</p>
            <input type="text" placeholder="Имя*" v-model="userFName">
            <p class="error">{{ error }}</p>
            <input type="text" placeholder="Отчество" v-model="userSName">
            <input type="date" placeholder="Дата рождения*" v-model="userDof">
            <p class="error">{{ error }}</p>
            <input type="tel" pattern="[7]{1}-[0-9{3}]-[0-9{3}]-[0-9{2}}]-[0-9{2}]" maxlength="11" placeholder="Номер телефона*" v-model="userTel">
            <p class="error">{{ error }}</p>
            <div class="gender">
                <p class="pe">Ваш пол:</p>
                <select v-model="userGen">
                    <option>Мужчина</option>
                    <option>Женщина</option>
                </select>
            </div>
            <div class="selector-group-client">
                <p class="pe">Группа клиентов*:</p>
                <p class="error">{{ error }}</p>
                <select multiple size="3" v-model="userGroupClient">
                    <option value="vip">VIP</option>
                    <option value="проблемные">Проблемные</option>
                    <option value="ОМС">ОМС</option>
                </select>
            </div>
            <div class="selector-therapist">
                <p class="pe">Лечащий врач:</p>
                <select v-model="userTherapist">
                    <option>Иванов</option>
                    <option>Захаров</option>
                    <option>Чернышева</option>
                </select>
            </div>
            <input 
            type="email" 
            placeholder="Почта" 
            v-model="userEmail"
            required email>
            <p class="error" v-if="required, email">Введите корректную почту</p>           
            <p class="pe">Не отправлять смс</p>
            <input type="checkbox" v-model="userSms">

            <div class="butn">
            <button @click="nextPage()" type="button">Дальше</button> 
            </div>
        </div>
        <div class="form-2" v-show="this.countPage == 2" >  
        <input type="number" placeholder="Индекс" v-model="userIndex">
        <input type="text" placeholder="Страна"v-model="userCountry">
        <input type="text" placeholder="Регион/Область" v-model="userRegion">
        <input type="text" placeholder="Город" v-model="userCity">
        <p class="error">{{ error }}</p>
        <input type="text" placeholder="Улица" v-model="userStreet">
        <input type="text" placeholder="Дом" v-model="userHome">
            <div class="butn">
                <button @click="backPage()" type="button">Назад</button>
                <button @click="nextPage()" type="button">Дальше</button> 
            </div>
        </div> 
        <div class="form-3" v-show="this.countPage == 3">
        <div class="typeDoc">
            <p class="pe">Тип документа*:</p>
            <select v-model="userTypeDoc">
                <option selected>Паспорт</option>
                <option>Свидетельство о рождении</option>
                <option>Водительское удостоверение</option>
            </select>
        </div>
        <input type="number" placeholder="Серия" v-model="userDocSer">
        <input type="number" placeholder="Номер" v-model="userDocNumb">
        <input type="text" placeholder="Кем выдан" v-model="userTo">
        <input type="text" placeholder="Дата выдачи*" v-model="userDocData">   
        <p class="error">{{ error }}</p>
        <div class="butn">
            <button @click="backPage()" type="button">Назад</button>
            <button @click="sendData()" type="button">Отправить</button> 
        </div>
        </div>
        <div class="form-complete" v-show="this.countPage == 4">
            <p>ВАША АНКЕТА УСПЕШНО ЗАПОЛНЕНА</p>
            <p>{{ dataUsers }}</p>
        </div>
    </form>
</mainInfoUser>
</template>

<script>
import { useVuelidate } from '@vuelidate/core';
import { required, email } from '@vuelidate/validators';

    export default {
        setup () {
            return { v$: useVuelidate() }
        },
    
        validations () {
            return {
            userFamily : {required},
            userFName : {required},
            userDof : {required},
            userTel : {required},
            userEmail: {email, required},
            userGroupClient : {required},
            userCity : {required},
            userTypeDoc : {required},
            userDocData : {required}
            }
        },
        data() {
            return {
        dataUsers : [],
        userFamily : '',
        userFName : '',
        userSName : '',
        userDof : '',
        userTel : '',
        userGen : [],
        userGroupClient : [],
        userTherapist : [],
        userSms : '',
        userEmail : '',
        userIndex : '',
        userCountry : '',
        userRegion : '',
        userCity : '',
        userStreet : '',
        userHome : '',
        userTypeDoc : '',
        userDocSer : '',
        userDocNumb : '',
        userTo : '',
        userDocData : '',
        error : '',
        countPage : 1,
        }
    },
    methods: {
        sendData() {
            if (this.userFamily == '') {
                return  this.error = 'Family not entered';
            } else if (this.userFName == '') {
                return this.error = 'First name not entered'
            } else if (this.userSName == '') {
                return this.error = 'Second name not entered'
            } else if (this.userEmail == '') {
                return this.error = 'Email not entered'
            }

            this.error = ""
           
            this.users.push({
                userFamily : this.userFamily,
                userFName : this.userFName,
                userSName : this.userSName,
                userDof : this.userDof,
                userTel : this.userTel,
                userGen : this.userGen,
                userGroupClient : this.userGroupClient,
                userTherapist : this.userTherapist,
                userEmail : this.userEmail,
            })
            this.countPage = 4
            console.log(this.countPage)
        },
        nextPage() {
            if (this.countPage < 3) {
               return this.countPage++}},
        backPage() {
            if (this.countPage > 1) {
            return this.countPage--}
        }
    }
}
</script>

<style scoped lang="scss">
* {
  padding: 0;
  margin: 0;
}

$cBlack: black;
$cWhite: white;

mainInfoUser {
  overflow: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  background: url(../img/image1.png) no-repeat;
  background-position: center;
}

.form-1, .form-2, .form-3, .form-4, .form-complete {
  /* display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column; */
  background: $cWhite;
  padding: 20px;
  border-radius: 10px;
  background: transparent;
  backdrop-filter: blur(15px);
  border: solid $cBlack;
}

.main-form {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
  width: 700px;
  height: 1000px;
  /* background: white;
  padding: 30px;
  border-radius: 10px; */
}

input {
  margin-bottom: 10px;
  width: 700px;
  height: 35px;
  outline: none;
  color: $cBlack;
  border-radius: 5px;
  border: solid $cBlack;
  text-align: center;
  font-size: 20px;

  &:focus::placeholder {
    border: solid $cWhite;
    color: $cWhite;
    background: $cBlack;
  }

  &::placeholder {
    color: $cBlack;
  }
}

.butn {
  display: flex;
  justify-content: center;

  button {
    border-radius: 10px;
    outline: none;
    border: none;
    width: 100px;
    height: 40px;
    margin: 10px;
    font-size: 18px;
    color: $cWhite;
    background: $cBlack;
    transition: all 0.3s ease;

    &:hover {
      color: $cBlack;
      background: $cWhite;
      border: solid $cBlack;
    }
  }
}

.pe {
  text-align: center;
  font-size: 18px;
  color: $cBlack;
  font-weight: 700;
}

select {
  width: 700px;
  height: 35px;
  outline: none;
  margin-bottom: 10px;
  border-radius: 5px;
  border: solid $cBlack;
  color: $cBlack;
  font-size: 20px;
  text-align: center;
}

.error {
  color: $cBlack;
  text-align: center;
  font-weight: 700;
  margin-bottom: 5px;
  text-shadow: $cBlack 5px;
}

.selector-therapist {
  p {
    font-size: 20px;
    font-weight: 600;
    color: $cBlack;
  }
}
</style>
