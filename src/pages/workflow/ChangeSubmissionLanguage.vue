<template>
	<SideModalBody>
		<template #pre-title>
			{{ props.submissionId }}
		</template>
		<template #title>
			{{ t('submission.list.changeSubmissionLanguage.title') }}
		</template>
		<template #description>
			{{ store.publicationTitle }}
		</template>
		<div class="p-4">
			<div class="bg-secondary p-4">
				<div id="changeSubmissionLanguage">
					<PkpForm
						v-bind="store.form"
						@set="store.setCustom"
						@success="store.success"
						@cancel="store.closeSideModal"
					></PkpForm>
				</div>
			</div>
		</div>
	</SideModalBody>
</template>

<script setup>
import {defineProps} from 'vue';
import PkpForm from '@/components/Form/Form.vue';
import SideModalBody from '@/components/Modal/SideModalBody.vue';
import {useChangeSubmissionLanguageStore} from '@/pages/workflow/changeSubmissionLanguageStore';

const props = defineProps({
	form: {
		type: Object,
		required: true,
	},
	publicationId: {
		type: Number,
		required: true,
	},
	submissionId: {
		type: Number,
		required: true,
	},
});
const store = useChangeSubmissionLanguageStore({
	form: props.form,
	publicationId: props.publicationId,
	submissionId: props.submissionId,
});
</script>
