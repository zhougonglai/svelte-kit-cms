<script>
	import BouncingLoader from '$lib/BouncingLoader.svelte';
	import Pagination from '$lib/Pagination.svelte';
	import { onMount } from 'svelte';

	let active = 'all';
	let games = [];
	let activeGames = [];
	let loading = true;
	let search = '';

	const types = [
		{
			key: 'all',
			label: '全部',
			games: () => games
		},
		{
			key: 'is_hot',
			label: '热门',
			games: () => games.filter(game => game.is_hot)
		},
		{
			key: 'is_free',
			label: '限免',
			games: () => games.filter(game => game.is_free)
		},
		{
			key: 'Steam',
			label: 'Steam',
			games: () => games.filter(game => game.game_label?.includes('Steam'))
		},
		{
			key: 'Origin',
			label: 'Origin',
			games: () => games.filter(game => game.game_label?.includes('Origin'))
		},
		{
			key: 'Uplay',
			label: 'Uplay',
			games: () => games.filter(game => game.game_label?.includes('Uplay'))
		},
		{
			key: 'xbox',
			label: 'xbox',
			games: () => games.filter(game => game.game_label?.includes('xbox'))
		},
		{
			key: 'ps4',
			label: 'ps4',
			games: () => games.filter(game => game.game_label?.includes('ps4'))
		},
		{
			key: 'Switch',
			label: 'Switch',
			games: () => games.filter(game => game.game_label?.includes('Switch'))
		}
	];

	const pagination = {
		total: 0,
		size: 40,
		index: 1
	};

	const switchActive = ({ key }) => {
		active = key;
		activeGames = types.find(type => type.key === key).games();
		pagination.index = 1;
		pagination.total = Math.ceil(activeGames.length / pagination.size);
	};

	const onPageChange = index => {
		pagination.index = index;
	};

	const onSearch = e => {
		search = e.target.value;
		pagination.total = Math.ceil(
			activeGames.filter(game => game.title.includes(search)).length /
				pagination.size
		);
	};

	async function getGames() {
		loading = true;
		activeGames = games = await fetch(
			`https://jiasu.bohe.com/config/game.json?${new URLSearchParams({
				lang: 'zh_CN',
				region_code: 1
			})}`
		).then(res => res.json());
		loading = false;
		pagination.total = Math.ceil(activeGames.length / pagination.size);
	}

	onMount(getGames);
</script>

<svelte:head>
	<title>游戏支持 - 薄荷BOHE加速器</title>
	<meta name="keywords" content="彩虹六号加速器、GTA5加速器、糖豆人加速器" />
	<meta
		name="description"
		content="薄荷加速器专业的网络游戏加速工具，完美加速漫威复仇者联盟、彩虹六号、GTA5、糖豆人、无限法则、NBA2K21、战地等上百款海外游戏，有效解决游戏中出现的延迟、丢包、卡顿等问题"
	/>
</svelte:head>

<section class="support mx-auto my-10">
	<div class="support-header flex justify-between">
		<ul class="support-tags flex gap-x-4">
			{#each types as type}
				<li
					class="support-tag cursor-pointer text-gray-800 opacity-75 hover:opacity-100"
					class:active={type.key === active}
					on:click={() => switchActive(type)}
				>
					{type.label}
				</li>
			{/each}
		</ul>

		<div class="support-search">
			<input
				class="search outline-none px-5 transition shadow hover:shadow-lg"
				type="search"
				list="games"
				placeholder="search"
				value={search}
				on:input={onSearch}
			/>
			<datalist id="games">
				{#each games as game}
					<option value={game.title} key={game.key} />
				{/each}
			</datalist>
		</div>
	</div>

	{#if loading}
		<BouncingLoader />
	{:else}
		<ul class="support-body grid grid-cols-5 content-start gap-5 mt-5">
			{#each activeGames
				.filter(game => game.title.includes(search))
				.slice(
					(pagination.index - 1) * pagination.size,
					pagination.index * pagination.size
				) as game}
				<li
					class="game select-none leading-10 height-10 truncate rounded px-2 cursor-pointer bg-white hover:shadow"
				>
					{game.title}
				</li>
			{/each}
		</ul>
	{/if}

	<Pagination {pagination} {onPageChange} class="justify-end" />
</section>

<style lang="scss">
	.support {
		width: 1200px;
		min-height: 600px;

		&-header {
			line-height: 40px;
			height: 40px;
		}

		&-tag {
			width: 60px;
			position: relative;
			text-align: center;
			&.active {
				opacity: 1;
				&::after {
					content: '';
					position: absolute;
					bottom: -5px;
					left: 0px;
					width: 60px;
					height: 4px;
					border-radius: 2px;
					background-color: var(--primary);
				}
			}
		}
		&-search {
			.search {
				width: 360px;
				border-radius: 20px;
			}
		}

		&-body {
			min-height: 460px;
			.game {
				&:hover {
					background-color: var(--primary);
				}
			}
		}
	}
</style>
