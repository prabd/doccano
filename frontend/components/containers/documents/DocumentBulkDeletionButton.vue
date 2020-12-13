<template>
  <div>
    <v-btn
      class="text-capitalize"
      outlined
      @click="dialog=true"
    >
      {{ $t('generic.deleteAll') }}
    </v-btn>
    <v-dialog
      v-model="dialog"
      width="800"
    >
      <confirm-form
        :items="items"
        :title="$t('dataset.deleteBulkDocumentsTitle')"
        :message="$t('dataset.deleteBulkDocumentsMessage')"
        :button-true-text="$t('generic.yes')"
        :button-false-text="$t('generic.cancel')"
        item-key="text"
        @ok="deleteAllDocuments($route.params.id);dialog=false"
        @cancel="dialog=false"
      />
      <!-- TODO: Change above ok function to deleteAll -->
    </v-dialog>
  </div>
</template>

<script>
import { mapState, mapGetters, mapActions } from 'vuex'
import ConfirmForm from '@/components/organisms/utils/ConfirmForm'

export default {
  components: {
    ConfirmForm
  },

  data() {
    return {
      dialog: false
    }
  },

  computed: {
    ...mapState('documents', ['selected', 'items']),
    ...mapGetters('documents', ['isDocumentSelected'])
  },

  methods: {
    // TODO: Make sure to get delete All function here
    ...mapActions('documents', ['deleteAllDocuments']),

    handleDeleteDocument() {
      const projectId = this.$route.params.id
      this.deleteDocument(projectId)
    }
  }
}
</script>
