<script>
	export let activity;
</script>

<li class="active flex px-4 hover:shadow  cursor-pointer overflow-hidden">
	<div class="cover flex place-content-center place-items-center">
		<img
			class="rounded"
			src={`${import.meta.env.VITE_SVELTEKIT_FILEPATH}${activity.image}`}
			alt={activity.title}
		/>
	</div>
	<div class="desc py-4 px-2 flex-1 flex flex-col justify-between">
		<div class="title text-lg font-bold">
			{activity.title}
		</div>
		<div class="summary flex-1 py-2 text-gray-500">
			{activity.summary}
		</div>
		<div class="status">
			<div
				class="tag text-sm px-2  inline-block rounded-sm"
				class:success={activity.is_recommend}
				class:disabled={!activity.is_recommend}
			>
				{activity.is_recommend ? '进行中' : '已结束'}
			</div>
			<time class="text-sm text-gray-500 ml-4"
				>{activity.start_time}~{activity.end_time}</time
			>
		</div>
	</div>
</li>

<style lang="scss">
	.active {
		.cover {
			width: 240px;
			height: 160px;
		}
		.tag {
			&.success {
				background-color: var(--primary);
			}
			&.disabled {
				background-color: gray;
			}
		}
	}
</style>
