<script setup>
// import { ref } from "vue";
import LoginModal from "./LoginModal.vue";
import CommentModal from "./CommentModal.vue";
import informations from "../../../public/informations.js";

</script>

<template>
	<v-sheet  v-for="information in informations" :key="information.id">
		<v-sheet
			class="my-3 d-flex flex-column py-3 v-rating"
			elevation="3"
			width="100%"
			rounded="2"
	>
		<h4 class="d-flex justify-center">Đánh giá & nhận xét</h4>

		<div class="d-flex align-center flex-column">
			<div class="text-h2 mt-3">
				{{ information.rating }}
				<span class="text-h6 ml-n3">/5</span>
			</div>

			<v-rating
				:model-value="information.rating"
				color="yellow-darken-3"
				size="large"
				readonly
				density="compact"
			></v-rating>
			<div class="px-3">{{ information.review }}</div>
		</div>

		<v-list
			bg-color="transparent"
			class="d-flex flex-column-reverse"
			density="compact"
		>
			<v-list-item
				v-for="(rating, i) in 5"
				:key="i"
			>
				<v-progress-linear
					:model-value="rating * 15"
					class="mx-n5"
					color="danger"
					height="8"
					rounded
				></v-progress-linear>
				<template v-slot:prepend>
					<span>{{ rating }}</span>
					<v-icon
						icon="mdi-star"
						color="yellow-darken-3"
						class="mx-2"
					></v-icon>
				</template>

				<template v-slot:append>
					<div class="rating-values">
						<span class="d-flex justify-end"> {{ rating * information.value }} </span>
					</div>
				</template>
			</v-list-item>
		</v-list>

		<v-sheet align="center">
			<p class="text-subtitle-1">Bạn đánh giá sao sản phẩm này ?</p>
			<LoginModal />
		</v-sheet>

		<v-container
			v-for="comment in information.comments"
			:key="comment.id"
		>
			<v-sheet class="d-flex justify-content-between py-2">
				<v-sheet class="d-flex align-center">
					<p class="bg-secondary rounded p-2">{{ comment.avatar }}</p>
					<h5 class="px-2">{{ comment.name }}</h5>
				</v-sheet>
				<p class="text-small">{{ comment.time }}</p>
			</v-sheet>

			<v-sheet
				class="p-2 text-small d-flex justify-center flex-column rounded"
				style="background-color: rgb(247, 243, 243); margin-left: 5%"
			>
				<p class="d-flex align-center">
					<b>Đánh giá:</b>
					<v-rating
						:model-value="comment.rating"
						color="yellow-darken-3"
						readonly
						density="compact"
						size="small"
						class="mx-2"
					>
					</v-rating>
				</p>
				<p class="more"><b>Nhận xét:</b> {{ comment.comment }}</p>
			</v-sheet>
		</v-container>

		<v-sheet class="mt-4">
			<CommentModal />
		</v-sheet>
	</v-sheet>
	</v-sheet>
</template>

<style>
.more {
	white-space: wrap;
	/* overflow: hidden; */
	/* text-overflow: ellipsis; */
}
</style>
