<template>
  <v-form
    method="POST"
    @submit.prevent="goToNextPage"
    style="max-width: 600px; margin: auto"
    ref="form"
  >
    <v-row v-show="is_register">
      <v-col cols="12">
        <div class="alertWarning">
          <div class="alertIcon">
            <img src="~/assets/images/warning_alert_icon.svg" />
          </div>
          <p class="alertContent">
            لطفا موارد زیر را به صورت دقیق تکمیل کنید، از این اطلاعات در جهت
            ارتباط با شما استفاده خواهد شد. همایش به صورت حضوری است.
          </p>
        </div>
      </v-col>
    </v-row>

    <v-row>
      <v-col cols="12" md="6">
        <v-text-field
          :rules="rules"
          solo
          flat
          hide-details="auto"
          :error-messages="error.first_name_persian"
          :error="!!error.first_name_persian"
          name="first_name_persian"
          v-model="userData.first_name_persian"
          placeholder="نام (فارسی)"
        >
          <template #label>
            نام (فارسی) <span style="color: red"><strong>* </strong></span>
          </template>
        </v-text-field>
      </v-col>
      <v-col cols="12" md="6">
        <v-text-field
          :rules="rules"
          solo
          flat
          hide-details="auto"
          :error-messages="error.last_name_persian"
          :error="!!error.last_name_persian"
          name="last_name_persian"
          v-model="userData.last_name_persian"
          placeholder="نام خانوادگی (فارسی)"
        >
          <template #label>
            نام خانوادگی (فارسی)
            <span style="color: red"><strong>* </strong></span>
          </template>
        </v-text-field>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12" md="6">
        <v-text-field
          dir="ltr"
          :rules="rules"
          solo
          flat
          hide-details="auto"
          :error-messages="error.first_name"
          :error="!!error.first_name"
          name="first_name"
          v-model="userData.first_name"
          placeholder="Name (english)"
        >
          <template #label>
            Name (english) <span style="color: red"><strong>* </strong></span>
          </template>
        </v-text-field>
      </v-col>
      <v-col cols="12" md="6">
        <v-text-field
          dir="ltr"
          :rules="rules"
          solo
          flat
          hide-details="auto"
          :error-messages="error.last_name"
          :error="!!error.last_name"
          name="last_name"
          v-model="userData.last_name"
          placeholder="Last Name (english)"
        >
          <template #label>
            Last Name (english)
            <span style="color: red"><strong>* </strong></span>
          </template>
        </v-text-field>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12" md="6">
        <v-text-field
          :rules="id_code_rules"
          solo
          flat
          hide-details="auto"
          :error-messages="error.national_code"
          :error="!!error.national_code"
          name="national_code"
          v-model="userData.national_code"
          placeholder="کد ملی"
          type="number"
        >
          <template #label>
            کد ملی <span style="color: red"><strong>* </strong></span>
          </template>
        </v-text-field>
      </v-col>
      <v-col cols="12" md="6">
        <v-select
          flat
          hide-details="auto"
          :error-messages="error.sex"
          :error="!!error.sex"
          v-model="userData.sex"
          solo
          placeholder="جنسیت"
          :items="['مرد', 'زن']"
          name="sex"
        >
          <template #label>
            جنسیت <span style="color: red"><strong>* </strong></span>
          </template>
        </v-select>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12" md="6">
        <v-input
          :rules="rules"
          solo
          flat
          type="number"
          hide-details="auto"
          :error-messages="error.birth_date"
          :error="!!error.birth_date"
          v-model="userData.birth_date"
          name="birth_date"
        >
          <date-picker
            style="width: 100%"
            v-model="userData.birth_date"
            placeholder="تاریخ تولد *"
          ></date-picker>
        </v-input>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12" md="6">
        <v-text-field
          disabled
          :rules="phone_rules"
          solo
          flat
          type="number"
          hide-details="auto"
          :error-messages="error.phone_number"
          :error="!!error.phone_number"
          name="phone_number"
          v-model="userData.phone_number"
          placeholder="شماره همراه دانش آموز (دارای واتساپ)"
        >
          <template #label>
            شماره همراه دانش آموز (دارای واتساپ)
            <span style="color: red"><strong>* </strong></span>
          </template>
        </v-text-field>
      </v-col>
      <v-col cols="12" md="6">
        <v-text-field
          :rules="phone_rules"
          solo
          flat
          type="number"
          hide-details="auto"
          :error-messages="error.parent_phone_number"
          :error="!!error.parent_phone_number"
          name="parent_phone_number"
          v-model="userData.parent_phone_number"
          placeholder="شماره یکی از والدین"
        >
          <template #label>
            شماره یکی از والدین
            <span style="color: red"><strong>* </strong></span>
          </template>
        </v-text-field>
      </v-col>
    </v-row>
    <v-row>
      <!--      <v-col cols="12" md="6">-->
      <!--        <v-text-field :rules="rules" solo flat type="number" :hide-details="!error.home_phone_number"-->
      <!--                      :error-messages="error.home_phone_number" :error="!!error.home_phone_number"-->
      <!--                      name="home_phone_number"-->
      <!--                      v-model="userData.home_phone_number"-->
      <!--                      placeholder="تلفن ثابت"
                <template #label>
            ناحیه<span  style="color: red"><strong>* </strong></span>
          </template>
        ><v-text-field/-->
      <!--      </v-col>-->
    </v-row>
    <v-row>
      <v-col cols="12" md="6">
        <v-select
          :error-messages="error.grade"
          :error="!!error.grade"
          hide-details="auto"
          v-model="userData.grade"
          :rules="rules"
          solo
          flat
          placeholder="پایه تحصیلی"
          :items="grade"
          name="grade"
        >
          <template #label>
            پایه تحصیلی <span style="color: red"><strong>* </strong></span>
          </template>
        </v-select>
      </v-col>
      <v-col cols="12" md="6">
        <v-text-field
          :rules="score_rules"
          solo
          flat
          type="number"
          step="0.01"
          hide-details="auto"
          :error-messages="error.before_grade_score"
          :error="!!error.before_grade_score"
          name="before_grade_score"
          v-model="userData.before_grade_score"
          placeholder="معدل پایه تحصیلی مرحله قبل"
        >
          <template #label>
            معدل پایه تحصیلی مرحله قبل
            <span style="color: red"><strong>* </strong></span>
          </template>
        </v-text-field>
      </v-col>
    </v-row>

    <v-row>
      <v-col cols="12" md="6">
        <v-text-field
          :rules="rules"
          solo
          flat
          hide-details="auto"
          :error-messages="error.school_name"
          :error="!!error.school_name"
          name="school_name"
          v-model="userData.school_name"
          placeholder="نام مدرسه"
        >
          <template #label>
            نام مدرسه <span style="color: red"><strong>* </strong></span>
          </template>
        </v-text-field>
      </v-col>
      <v-col cols="12" md="6">
        <v-text-field
          :rules="rules"
          solo
          flat
          hide-details="auto"
          :error-messages="error.aria"
          :error="!!error.aria"
          name="aria"
          v-model="userData.aria"
          placeholder="ناحیه"
        >
          <template #label>
            ناحیه <span style="color: red"><strong>* </strong></span>
          </template>
        </v-text-field>
      </v-col>
    </v-row>
    <div
      v-show="is_register"
      style="
        display: flex;
        flex-direction: row-reverse;
        justify-content: space-between;
        margin-top: 30px;
      "
    >
      <v-btn class="button-fill next-btn" v-on:click="goToNextPage()"
        >مرحله بعد</v-btn
      >
    </div>
  </v-form>
</template>

<script>
import Form from "@/pages/register/form";

export default {
  name: "user_info",
  components: { Form },
  data() {
    return {
      male_junior_reg: false,
      female_junior_reg: false,
      userData: this.$auth.loggedIn
        ? { ...this.$auth.user }
        : { ...this.$store.state.register.userData },
      rules: [(v) => !!v || "این مقدار لازم است"],
      score_rules: [
        (v) => !!v || "این مقدار لازم است",
        (v) => (v >= 0 && v <= 20) || "این مقدار باید بین 0 و 20 باشد",
      ],
      phone_rules: [
        (v) => !!v || "این مقدار لازم است",
        (v) => (!!v && v.length === 11) || "شماره وارد شده باید 11 رقمی باشد",
        (v) => (!!v && v > 0) || "کاراکتر غیر مجاز",
      ],
      id_code_rules: [
        (v) => !!v || "این مقدار لازم است",
        (v) => (!!v && v.length === 10) || "کد ملی وارد شده باید 10 رقمی باشد",
        (v) => (!!v && v > 0) || "کاراکتر غیر مجاز",
      ],
    };
  },
  methods: {
    async goToNextPage() {
      if (this.$refs.form.validate())
        this.$store.commit(
          "register/setState",
          this.$store.state.register.state + 1
        );
    },
  },
  computed: {
    error() {
      return this.$store.state.register.error;
    },
    state: {
      get() {
        return this.$store.state.register.state;
      },
      set(data) {
        return this.$store.commit("register/setState", data);
      },
    },
    grade() {
      let grades = {
        1: ["هفتم", "هشتم", "نهم", "دهم", "یازدهم", "دوازدهم"],
        2: ["دهم", "یازدهم", "دوازدهم"],
      };
      let t = this;
      if (
        (t.male_junior_reg && t.userData.sex == "مرد") ||
        (t.female_junior_reg && t.userData.sex == "زن")
      )
        return grades["1"];
      else if (
        (!t.male_junior_reg &&
          t.userData.sex == "مرد" &&
          ["هفتم", "هشتم", "نهم"].includes(t.userData.grade)) ||
        (!t.female_junior_reg &&
          t.userData.sex == "زن" &&
          ["هفتم", "هشتم", "نهم"].includes(t.userData.grade))
      )
        t.userData.grade = undefined;

      return grades["2"];
    },
  },
  watch: {
    userData: {
      handler: function (val, oldVal) {
        this.$store.commit("register/setUserData", val);
      },
      deep: true,
    },
  },
  props: {
    is_register: { default: true },
  },
  beforeMount() {
    let t = this;
    this.$axios
      .get("get_option/male_aval_reg")
      .then(
        (res) => (t.male_junior_reg = res.data.value === "close" ? false : true)
      );
    this.$axios
      .get("get_option/female_aval_reg")
      .then(
        (res) =>
          (t.female_junior_reg = res.data.value === "close" ? false : true)
      );
  },
};
</script>

<style scoped>
.alertWarning {
  border: 2px solid #fb8c00;
  border-radius: 10px;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 10px;
  gap: 20px;
}

.alertContent {
  font-style: normal;
  font-weight: 700;
  font-size: 16px;
  text-align: right;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0px;

  color: #fb8c00;
}

@media screen and (min-width: 1000px) {
  .next-btn {
    transform: translateX(-50px) scale(1.2);
    border-radius: 12px;
  }
}
</style>
