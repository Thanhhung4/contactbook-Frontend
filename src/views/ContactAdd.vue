<template>
  <div class="page">
    <h4>Thêm Liên hệ</h4>
    <ContactForm :contact="form" @submit:contact="addContact" />
    <p>{{ message }}</p>
  </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";

export default {
  components: {
    ContactForm,
  },
  data() {
    return {
      form: {
        name: this.contact?.name || "",
        email: this.contact?.email || "",
        address: this.contact?.address || "",
        phone: this.contact?.phone || "",
        favorite: this.contact?.favorite || false,
      },
      message: ""
    };
  },
  props: {
    contact: {
      type: Object,
      default: () => ({
        name: "",
        email: "",
        address: "",
        phone: "",
        favorite: false,
      }),
    },
  },
  methods: {
    async addContact(data) {
      try {
        await ContactService.create(data);
        alert("Liên hệ được thêm thành công.");
        this.$router.push({ name: "contactbook" });
      } catch (error) {
        console.log(error);
        this.message = "Đã xảy ra lỗi khi thêm liên hệ.";
      }
    },
  },
};
</script>