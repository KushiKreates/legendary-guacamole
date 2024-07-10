<script>
    import { getContext } from 'svelte';
    import Database from './Settings/Database.svelte';
    import General from './Settings/General.svelte';
    import Users from './Settings/Users.svelte';
    import Pipelines from './Settings/Pipelines.svelte';
    import Audio from './Settings/Audio.svelte';
    import Images from './Settings/Images.svelte';
    import Interface from './Settings/Interface.svelte';
    import Models from './Settings/Models.svelte';
    import Connections from './Settings/Connections.svelte';
    import Documents from './Settings/Documents.svelte';
    import WebSearch from './Settings/WebSearch.svelte';
    import { config } from '$lib/stores';
    import { getBackendConfig } from '$lib/apis';

    const i18n = getContext('i18n');
    let selectedTab = 'general';
</script>

<div class="flex flex-col lg:flex-row w-full h-full py-2 lg:space-x-4">
    <div class="tabs flex flex-row overflow-x-auto space-x-1 max-w-full lg:space-x-0 lg:space-y-1 lg:flex-col lg:flex-none lg:w-44 dark:text-gray-200 text-xs text-left scrollbar-none">
        <button class="tab-button {selectedTab === 'general' ? 'active-tab' : 'inactive-tab'}" on:click={() => selectedTab = 'general'}>
            <div class="icon-container">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16" fill="currentColor" class="w-4 h-4">
                    <path fill-rule="evenodd" d="M6.955 1.45A.5.5 0 0 1 7.452 1h1.096a.5.5 0 0 1 .497.45l.17 1.699c.484.12.94.312 1.356.562l1.321-1.081a.5.5 0 0 1 .67.033l.774.775a.5.5 0 0 1 .034.67l-1.08 1.32c.25.417.44.873.561 1.357l1.699.17a.5.5 0 0 1 .45.497v1.096a.5.5 0 0 1-.45.497l-1.699.17c-.12.484-.312.94-.562 1.356l1.082 1.322a.5.5 0 0 1-.034.67l-.774.774a.5.5 0 0 1-.67.033l-1.322-1.08c-.416.25-.872.44-1.356.561l-.17 1.699a.5.5 0 0 1-.497.45H7.452a.5.5 0 0 1-.497-.45l-.17-1.699a4.973 4.973 0 0 1-1.356-.562L4.108 13.37a.5.5 0 0 1-.67-.033l-.774-.775a.5.5 0 0 1-.034-.67l1.08-1.32a4.971 4.971 0 0 1-.561-1.357l-1.699-.17A.5.5 0 0 1 1 8.548V7.452a.5.5 0 0 1 .45-.497l1.699-.17c.12-.484.312-.94.562-1.356L2.629 4.107a.5.5 0 0 1 .034-.67l.774-.774a.5.5 0 0 1 .67-.033L5.43 3.71a4.97 4.97 0 0 1 1.356-.561l.17-1.699ZM6 8c0 .538.212 1.026.558 1.385l.057.057a2 2 0 0 0 2.828-2.828l-.058-.056A2 2 0 0 0 6 8Z" clip-rule="evenodd"/>
                </svg>
            </div>
            <div class="text-container">{$i18n.t('General')}</div>
        </button>

        <button class="tab-button {selectedTab === 'users' ? 'active-tab' : 'inactive-tab'}" on:click={() => selectedTab = 'users'}>
            <div class="icon-container">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16" fill="currentColor" class="w-4 h-4">
                    <path d="M8 8a2.5 2.5 0 1 0 0-5 2.5 2.5 0 0 0 0 5ZM3.156 11.763c.16-.629.44-1.21.813-1.72a2.5 2.5 0 0 0-2.725 1.377c-.136.287.102.58.418.58h1.449c.01-.077.025-.156.045-.237ZM12.847 11.763c.02.08.036.16.046.237h1.446c.316 0 .554-.293.417-.579a2.5 2.5 0 0 0-2.722-1.378c.374.51.653 1.09.813 1.72ZM14 7.5a1.5 1.5 0 1 1-3 0 1.5 1.5 0 0 1 3 0ZM3.5 9a1.5 1.5 0 1 0 0-3 1.5 1.5 0 0 0 0 3ZM5 13c-.552 0-1.013-.455-.876-.99a4.002 4.002 0 0 1 7.753 0c.136.535-.324.99-.877.99H5Z"/>
                </svg>
            </div>
            <div class="text-container">{$i18n.t('Users')}</div>
        </button>

        <button class="tab-button {selectedTab === 'connections' ? 'active-tab' : 'inactive-tab'}" on:click={() => selectedTab = 'connections'}>
            <div class="icon-container">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 16 16" fill="currentColor" class="w-4 h-4">
                    <path d="M1 9.5A3.5 3.5 0 0 0 4.5 13H12a3 3 0 0 0 .917-5.857 2.503 2.503 0 0 0-3.198-3.019 3.5 3.5 0 0 0-6.628 2.171A3.5 3.5 0 0 0 1 9.5Z"/>
                </svg>
            </div>
            <div class="text-container">{$i18n.t('Connections')}</div>
        </button>

        <button class="tab-button {selectedTab === 'models' ? 'active-tab' : 'inactive-tab'}" on:click={() => selectedTab = 'models'}>
            <div class="icon-container">
                <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20" fill="currentColor" class="w-4 h-4">
                    <path fill-rule="evenodd" d="M10 1c3.866 0 7 1.79 7 4s-3.134 4-7 4-7-1.79-7-4 3.134-4 7-4zm5.694 8.13c.464-.264.91-.583 1.306-.952V10c0 2.21-3.134 4-7 4s-7-1.79-7-4V8.178c.396.37.842.688 1.306.953C5.838 10.006 7.854 10.5 10 10.5s4.162-.494 5.694-1.37zM3 13.179V15c0 2.21 3.134 4 7 4s7-1.79 7-4v-1.822c-.396.37-.842.688-1.306.953C14.162 14.506 12.146 15 10 15s-4.162-.494-5.694-1.37c-.464-.264-.91-.583-1.306-.952z" clip-rule="evenodd"/>
                </svg>
            </div>
            <div class="text-container">{$i18n.t('Models')}</div>
        </button>
    </div>

    <div class="settings-content">
        {#if selectedTab === 'general'}
            <General {config} />
        {:else if selectedTab === 'users'}
            <Users {config} />
        {:else if selectedTab === 'connections'}
            <Connections {config} />
        {:else if selectedTab === 'models'}
            <Models {config} />
        {/if}
    </div>
</div>

<style>
    .tab-button {
        display: flex;
        align-items: center;
        justify-content: flex-start;
        padding: 0.5rem 1rem;
        background-color: transparent;
        border: none;
        cursor: pointer;
        transition: background-color 0.3s ease;
    }
    .active-tab {
        background-color: var(--color-active-tab);
    }
    .inactive-tab:hover {
        background-color: var(--color-hover-tab);
    }
    .icon-container {
        margin-right: 0.5rem;
    }
    .text-container {
        flex: 1;
    }
    .settings-content {
        flex: 1;
        padding: 1rem;
    }
</style>
