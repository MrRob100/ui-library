<template>
	<span class="multilingualProgress" :class="classes">
		<button
			v-tooltip="{
				content: tooltip,
				theme: 'pkp-tooltip',
			}"
			type="button"
			aria-hidden="true"
			@click.prevent
		>
			<Icon icon="globe" />
		</button>
		<span class="-screenReader">{{ tooltip }}</span>
	</span>
</template>

<script>
import Icon from '@/components/Icon/Icon.vue';

export default {
	name: 'MultilingualProgress',
	components: {Icon},
	props: {
		/** The number of completed multilingual items.  */
		count: {
			type: Number,
			required: true,
		},
		/** The total number of multilingual items available to be completed. */
		total: {
			type: Number,
			required: true,
		},
	},
	computed: {
		/**
		 * Classes to add to the wrapper element
		 *
		 * @return {Array}
		 */
		classes() {
			let classes = [];
			if (this.count === this.total) {
				classes.push('multilingualProgress--isComplete');
			} else if (!this.count) {
				classes.push('multilingualProgress--isEmpty');
			} else {
				classes.push('multilingualProgress--isIncomplete');
			}
			return classes;
		},

		/**
		 * Tooltip
		 *
		 * @return {String}
		 */
		tooltip() {
			return this.t('form.multilingualProgress', {
				count: this.count,
				total: this.total,
			});
		},
	},
};
</script>

<style lang="less">
@import '../../styles/_import';

.multilingualProgress {
	display: inline-block;
	line-height: @line-sml;
	vertical-align: middle;

	button {
		border: none;
		background: none;
		padding: 0;
		cursor: pointer;
	}

	.fa {
		font-size: @line-sml;
	}
}

.multilingualProgress--isEmpty .fa {
	color: @text-light;
}

.multilingualProgress--isIncomplete .fa {
	color: @no;
}

.multilingualProgress--isComplete .fa {
	color: @yes;
}
</style>
