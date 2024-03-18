<template>
<div v-if="contact" class="page">
<h4>Thêm liên hệ mới</h4>
<ContactForm :contact="contact" @submit:contact="createContact"
@delete:contact="deleteContact" />
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
      contact: {},
      message: "",
    };
  },
  methods: {
    async createContact(data) {
      try {
        await ContactService.create(data); 
        alert('Liên hệ được thêm thành công.');
        this.$router.push({ name: "contactbook" });
      } catch (error) {
        console.error(error);
      }
    },
    created() {
      this.message = "";
    },
  },
};
</script>