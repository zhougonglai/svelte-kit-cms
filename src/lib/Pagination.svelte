<script>
	export let pagination;
	export let onPageChange;
</script>

{#if pagination.total}
	<ul class={['pagination mt-4 gap-x-4 flex', $$restProps?.class].join(' ')}>
		<li class="pagination-item">
			<button
				disabled={pagination.index === 1}
				on:click={() => onPageChange(1)}
			>
				首页
			</button>
		</li>
		<li class="pagination-item">
			<button
				disabled={pagination.index === 1}
				on:click={() => onPageChange(pagination.index - 1)}
			>
				上一页
			</button>
		</li>
		{#if pagination.total >= 7}
			{#if pagination.index <= 4}
				{#each Array(pagination.index + 1).fill(pagination.index) as page, index}
					<li class="pagination-item">
						<button
							class:active={pagination.index === index + 1}
							on:click={() => onPageChange(index + 1)}>{index + 1}</button
						>
					</li>
				{/each}
			{:else}
				<li class="pagination-item">
					<button on:click={() => onPageChange(1)}>1</button>
				</li>
				<li class="pagination-item">...</li>
			{/if}

			{#if pagination.index > 4 && pagination.index < pagination.total - 3}
				{#each [pagination.index - 2, pagination.index - 1, pagination.index, pagination.index + 1, pagination.index + 2] as page}
					<li class="pagination-item">
						<button
							class:active={pagination.index === page}
							on:click={() => onPageChange(page)}>{page}</button
						>
					</li>
				{/each}
			{/if}

			{#if pagination.index >= pagination.total - 3}
				{#each Array(pagination.total)
					.fill(pagination.index)
					.map((p, i) => i + 1)
					.slice(pagination.index - 3, pagination.total) as page}
					<li class="pagination-item">
						<button
							class:active={pagination.index === page}
							on:click={() => onPageChange(page)}>{page}</button
						>
					</li>
				{/each}
			{:else}
				<li class="pagination-item">...</li>
				<li class="pagination-item">
					<button on:click={() => onPageChange(pagination.total)}
						>{pagination.total}</button
					>
				</li>
			{/if}
		{:else}
			{#each Array(pagination.total)
				.fill(pagination.total)
				.map((p, i) => i + 1) as page}
				<li class="pagination-item">
					<button
						class:active={pagination.index === page}
						on:click={() => onPageChange(page)}>{page}</button
					>
				</li>
			{/each}
		{/if}
		<li class="pagination-item">
			<button
				disabled={pagination.total === pagination.index}
				on:click={() => onPageChange(pagination.index + 1)}
			>
				下一页
			</button>
		</li>
		<li class="pagination-item">
			<button
				disabled={pagination.total === pagination.index}
				on:click={() => onPageChange(pagination.total)}
			>
				末页
			</button>
		</li>
	</ul>
{/if}

<style lang="scss">
	.pagination {
		&-item {
			button {
				padding: 0.25rem 0.75rem;
				outline: none;
				border-radius: 2px;
				&:disabled {
					color: gray;
					cursor: not-allowed;
				}
				&:not(:disabled).active {
					background-color: var(--primary);
					color: white;
				}
				&:not(.active, :disabled):hover {
					color: var(--primary);
				}
			}
		}
	}
</style>
