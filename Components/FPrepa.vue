<script>
import axios from "axios";
import FHeader from "./Info-form/FHeader.vue";
import FTitle from "./utils/FTitle.vue";
import FButtom from "./utils/FButtom.vue";
import FCancel from "./utils/FCancel.vue";
import FInput from "./utils/FInput.vue";
import FTextArea from "./utils/FTextArea.vue";
import FText from "./utils/FText.vue";
import FDate from "./Info-form/FDate.vue";
import FBannner from "./utils/FBanner.vue";
import FNotes from "./Info-form/FNotes.vue";
import FSignature from "./utils/FSignature.vue";
import FRecommendations from "./Info-form/FRecommendations.vue";
import FSelectionInput from "./utils/FSelectionInput.vue";
import FSelection from "./utils/FSelection.vue";

export default {
  components: {
    FTitle,
    FButtom,
    FCancel,
    FInput,
    FTextArea,
    FText,
    FDate,
    FNotes,
    FSignature,
    FRecommendations,
    FSelectionInput,
    FBannner,
    FHeader,
    FSelection,
  },
  data() {
    return {
      healFormSecu: {
        studentName: "",
        grade: "",
        bloodGroup: "",
        mother: "",
        phoneMother: "",
        father: "",
        phoneFather: "",
        address: "",
        homePhone: "",
        officePhone: "",
        additionalAddress: "",
        additionalHomePhone: "",
        emergencyPerson: "",
        emergencyPhone: "",
        emergencyPhone1: "",
        emergencyPhone2: "",
        doctorsName: "",
        doctorsPhone: "",
        doctorsPhoneOffice: "",
        allDayPhone: "",
        condition: "",
        treatment: "",
        dosage: "",
        medication: "",
        allergies: "",
        vaccines: "",
        covidVaccines: "",
        hadCovid: "",
        importInfo: "",
        signature: "",
      },
      formSubmitSuccess: false,
      formSubmitError: false,
    };
  },
  created() {
    this.studentInfo();
  },
  methods: {
    async studentInfo() {
      try {
        const requestBody = {
          q: "MTk2OTpNVGsyT1Rwb2ZIaGxTSDQzVmtWMQ==",
        };
        const response = await axios.post(
          "https://backend.schoolaid.app/med",
          requestBody,
          {
            headers: {
              "x-api-key": "4LbhvqUAA68LlKXUKl5VT80HbPwvultf2EmBN2qy",
            },
          }
        );

        const studentName = response.data.body.studentName;
        const grade = response.data.body.grade;

        this.healFormSecu.studentName = studentName;
        this.healFormSecu.grade = grade;
      } catch (error) {}
    },

    async submitForm() {
      try {
        await this.studentInfo();
        const response = await axios.put(
          "https://backend.schoolaid.app/med",
          this.healFormSecu,
          {
            headers: {
              "x-api-key": "4LbhvqUAA68LlKXUKl5VT80HbPwvultf2EmBN2qy",
            },
          }
        );

        if (response.status === 200) {
          console.log("res:", this.healFormSecu);

          this.formSubmitSuccess = true;
          this.formSubmitError = false;
        } else {
          this.formSubmitSuccess = false;
          this.formSubmitError = true;
        }
      } catch (error) {
        console.error("Error al enviar el formulario:", error);
        console.log("res on error:", this.healFormSecu);
        this.formSubmitSuccess = false;
        this.formSubmitError = true;
      }
    },
  },
};
</script>
<template>
  <section>
    <FHeader />
  </section>
  <form class="pb-8" @submit.prevent="submitForm">
    <div class="container mx-auto rounded">
      <FTitle title="Formulario de Secundaria y Prepa" />
      <div class="mx-auto">
        <div class="xl:mx-0">
          <FBannner />
          <div class="py-12 grid md:grid-cols-2 grid-cols-1 gap-4">
            <div class="flex flex-col mb-6 px-4 pt-4">
              <label for="Name" class="pb-2 text-sm font-bold text-gray-800"
                >Nombre del Alumno</label
              >
              <div class="border border-gray-300 shadow-sm rounded flex">
                <div
                  class="focus:outline-none px-4 py-3 flex items-center border-r border-gray-300 text-xl"
                >
                  <i class="fa fa-user"></i>
                </div>
                <p
                  id="name"
                  name="name"
                  class="pl-3 py-3 w-full text-sm focus:outline-none placeholder-gray-500 rounded bg-transparent text-gray-600"
                >
                  {{ healFormSecu.studentName }}
                </p>
              </div>
            </div>
            <div class="flex flex-col mb-6 px-4 pt-4">
              <label for="Section" class="pb-2 text-sm font-bold text-gray-800"
                >Grado y Sección</label
              >
              <div class="border border-gray-300 shadow-sm rounded flex">
                <div
                  class="focus:outline-none px-4 py-3 flex items-center border-r border-gray-300 text-xl"
                >
                  <i class="fa fa-clipboard-list"></i>
                </div>
                <p
                  id="section"
                  name="section"
                  class="pl-3 py-3 w-full text-sm focus:outline-none placeholder-gray-500 rounded bg-transparent text-gray-600"
                >
                  {{ healFormSecu.grade }}
                </p>
              </div>
            </div>
            <FInput
              label="Adjuntar Grupo Sanguíneo"
              for="bloodGroup"
              type="text"
              id="bloodGroup"
              name="bloodGroup"
              placeholder="Grupo Sanguíneo"
              @update:value="healFormSecu.bloodGroup = $event"
              required
            />
          </div>
        </div>
      </div>
    </div>
    <div class="container mx-auto bg-white rounded">
      <FTitle title="Información Familiar" />
      <div class="pt-4">
        <div class="container">
          <div class="my-6 grid md:grid-cols-2 grid-cols-1 gap-4">
            <FInput
              label="Nombre de la Madre"
              for="mother"
              type="text"
              id="mother"
              name="mother"
              placeholder="Nombre de la Madre"
              @update:value="healFormSecu.mother = $event"
              required
            />
            <FInput
              label="Celular de la Madre"
              for="phoneMother"
              type="phone"
              id="phoneMother"
              name="phoneMother"
              placeholder="Celular de la Madre"
              @update:value="healFormSecu.phoneMother = $event"
              required
            />
            <FInput
              label="Nombre del Padre"
              for="father"
              type="text"
              id="father"
              name="father"
              placeholder="Nombre del Padre"
              @update:value="healFormSecu.father = $event"
              required
            />
            <FInput
              label="Celular del Padre"
              for="phoneFather"
              type="phone"
              id="phoneFather"
              name="phoneFather"
              placeholder="Celular del Padre"
              @update:value="healFormSecu.phoneFather = $event"
              required
            />
            <div class="grid grid-cols-1">
              <FInput
                label="Dirección"
                for="address"
                type="text"
                id="address"
                name="address"
                placeholder="Dirección"
                @update:value="healFormSecu.address = $event"
                required
              />
            </div>
            <div class="grid md:grid-cols-2 grid-cols-1 gap-4">
              <FInput
                label="Teléfono de Casa"
                for="homePhone"
                type="phone"
                id="homePhone"
                name="homePhone"
                placeholder="Teléfono de Casa"
                @update:value="healFormSecu.homePhone = $event"
                required
              />
              <FInput
                label="Teléfono de Oficina"
                for="officePhone"
                type="phone"
                id="officePhone"
                name="officePhone"
                placeholder="Teléfono de Oficina"
                @update:value="healFormSecu.officePhone = $event"
                required
              />
            </div>
            <FInput
              label="Dirección Adicional"
              for="additionalAddress"
              type="text"
              id="additionalAddress"
              name="additionalAddress"
              placeholder="Dirección Adicional"
              @update:value="healFormSecu.additionalAddress = $event"
            />
            <FInput
              label="Teléfono Adicional"
              for="additionalHomePhone"
              type="phone"
              id="additionalHomePhone"
              name="additionalHomePhone"
              placeholder="Teléfono Adicional"
              @update:value="healFormSecu.additionalHomePhone = $event"
              required
            />
          </div>
        </div>
      </div>
    </div>
    <div class="container mx-auto bg-white rounded">
      <FTitle title="Contactos de Emergencia" />
      <div class="pt-4">
        <div class="container">
          <div class="my-6 grid md:grid-cols-2 grid-cols-1 gap-4">
            <FInput
              label="Contacto en caso de emergencia"
              for="emergencyPerson"
              type="text"
              id="emergencyPerson"
              name="emergencyPerson"
              placeholder="Contacto de emergencia"
              @update:value="healFormSecu.emergencyPerson = $event"
              required
            />
            <FInput
              label="Teléfono en caso de emergencia"
              for="emergencyPhone"
              type="phone"
              id="emergencyPhone"
              name="emergencyPhone"
              placeholder="Teléfono en caso de emergencia"
              @update:value="healFormSecu.emergencyPhone = $event"
            />
            <FInput
              label="Teléfono en caso de emergencia"
              for="emergencyPhone1"
              type="phone"
              id="emergencyPhone1"
              name="emergencyPhone1"
              placeholder="Teléfono en caso de emergencia"
              @update:value="healFormSecu.emergencyPhone1 = $event"
            />
            <FInput
              label="Teléfono en caso de emergencia"
              for="emergencyPhone2"
              type="phone"
              id="emergencyPhone2"
              name="emergencyPhone2"
              placeholder="Teléfono en caso de emergencia"
              @update:value="healFormSecu.emergencyPhone2 = $event"
              required
            />
          </div>
        </div>
      </div>
    </div>
    <div class="container mx-auto bg-white rounded">
      <FTitle title="Información Importante" />
      <div class="pt-4">
        <div class="container">
          <div class="my-6 grid md:grid-cols-2 grid-cols-1 gap-4">
            <FInput
              label="Nombre del Médico"
              for="doctorsName"
              type="text"
              id="doctorsName"
              name="doctorsName"
              placeholder="Nombre del Médico"
              @update:value="healFormSecu.doctorsName = $event"
              required
            />
            <FInput
              label="Celular del Médico"
              for="doctorsPhone"
              type="phone"
              id="doctorsPhone"
              name="doctorsPhone"
              placeholder="Celular del Médico"
              @update:value="healFormSecu.doctorsPhone = $event"
              required
            />
            <FInput
              label="Teléfono del Consultorio"
              for="doctorsPhoneOffice"
              type="phone"
              id="doctorsPhoneOffice"
              name="doctorsPhoneOffice"
              placeholder="Teléfono del Consultorio"
              @update:value="healFormSecu.doctorsPhoneOffice = $event"
              required
            />
            <FInput
              label="Teléfono 24 horas"
              for="allDayPhone"
              type="phone"
              id="allDayPhone"
              name="allDayPhone"
              placeholder="Teléfono 24 horas"
              @update:value="healFormSecu.allDayPhone = $event"
              required
            />
            <FSelectionInput
              label="¿Su hijo tiene algún padecimiento que requiera tratamiento?"
              for="condition"
              type="text"
              id="condition"
              name="condition"
              placeholder="¿Cuál?"
              @update:value="healFormSecu.condition = $event"
              required
            />
            <FSelectionInput
              label="¿Qué tratamiento requiere?"
              for="treatment"
              type="text"
              id="treatment"
              name="treatment"
              placeholder="¿Cuál?"
              @update:value="healFormSecu.treatment = $event"
              required
            />
            <FSelectionInput
              label="¿Qué dosis necesita con dicho tratamiento, si fuera requerido?"
              for="dosage"
              type="text"
              id="dosage"
              name="dosage"
              placeholder="¿Cuál?"
              @update:value="healFormSecu.dosage = $event"
              required
            />
            <FSelectionInput
              label="¿Está tomando algún medicamento?"
              for="medication"
              type="text"
              id="medication"
              name="medication"
              placeholder="¿Cuál?"
              @update:value="healFormSecu.medication = $event"
              required
            />
            <FSelectionInput
              label="¿Su hijo tiene alguna alergia?"
              description="Especificar:"
              for="allergies"
              type="text"
              id="allergies"
              name="allergies"
              placeholder="¿Cuál?"
              @update:value="healFormSecu.allergies = $event"
              required
            />
            <FSelectionInput
              label="¿Se encuentra al corriente de sus vacunas?"
              description="Fecha de su última vacuna de tétanos:"
              for="vaccines"
              type="date"
              id="vaccines"
              name="vaccines"
              @update:value="healFormSecu.vaccines = $event"
              required
            />
            <FSelectionInput
              label="¿Está vacunado de covid?"
              description="¿Dosis de vacunas contra el covid?:"
              for="covidVaccines"
              type="text"
              id="covidVaccines"
              name="covidVaccines"
              placeholder="¿Hasta cuál dosis?"
              @update:value="healFormSecu.covidVaccines = $event"
              required
            />
            <FSelectionInput
              label="¿Ha tenido covid?"
              description="Especificar hace cuánto tuve covid:"
              for="hadCovid"
              type="text"
              id="hadCovid"
              name="hadCovid"
              placeholder="¿Cuándo?"
              @update:value="healFormSecu.hadCovid = $event"
              required
            />
            <FTextArea
              label="¿Desea adjuntar alguna observación importante?"
              for="importInfo"
              id="importInfo"
              name="importInfo"
              @update:value="healFormSecu.importInfo = $event"
              placeholder="Adjunta alguna observación"
            />
          </div>
        </div>
      </div>
    </div>
    <div class="container mx-auto bg-white rounded">
      <FTitle title="Notas" />
      <FNotes />
    </div>
    <div class="container mx-auto">
      <div class="my-6">
        <FDate />
        <FSignature
          label="Firma del encargado"
          :modelValue="healFormSecu.signature"
          @update:modelValue="
            (signature) => (healFormSecu.signature = signature)
          "
          required
        />
      </div>
      <div class="flex items-start">
        <div v-if="formSubmitSuccess" class="alert-success">
          Formulario enviado exitosamente.
        </div>
        <div v-if="formSubmitError" class="alert-danger">
          Error al enviar el formulario. Por favor, inténtalo de nuevo más
          tarde.
        </div>
      </div>
    </div>
    <div class="container mx-auto w-11/12 xl:w-full px-4">
      <div class="w-full py-4 sm:px-0 bg-white flex justify-end">
        <FCancel />
        <FButtom />
      </div>
    </div>
  </form>
</template>
