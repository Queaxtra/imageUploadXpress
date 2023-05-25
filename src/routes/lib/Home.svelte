<script>
    import toast, { Toaster } from 'svelte-french-toast';
    let fileInput = "";
    import { Storage, Client } from 'appwrite';
    import Info from './Info.svelte';
    const client = new Client();
    client.setEndpoint('https://cloud.appwrite.io/v1').setProject(import.meta.env.VITE_APP_KEY);
    const storage = new Storage(client);
    const code = Math.floor(Math.random() * 1000000 + 1);

    async function uploadFile() {
        const promise = storage.createFile('1001', `${code}`, document.getElementById('fileUpload').files[0]);
        promise.then(function (response) {
            toast.success('File uploaded successfully!', {
                position: "top-right"
            })
        }, function (error) {
            toast.error('File upload failed!', {
                position: "top-right"
            })
        });
    }
</script>

<Toaster />
<div>
    <h2 class="text-center relative top-40 text-3xl font-bold">imageUploadXpress</h2>
    <img class="ml-auto mr-auto left-10 right-0 w-44 relative top-40" src="https://i.hizliresim.com/mt5iy8o.png" alt="line">

    <div class="w-80 md:w-96 lg:w-96 h-72 bg-[#f0f0f0]/50 my-auto mx-auto flex justify-center items-center mt-52 rounded">
        <label class="w-64 flex flex-col items-center px-4 py-6 border-dashed text-blue-500 rounded tracking-wide uppercase border border-blue-500 cursor-pointer">
            <i class="fa-solid fa-upload text-xl"></i>
            <span class="mt-2 text-base leading-normal">Choose File</span>
            <input bind:value={fileInput} type="file" id="fileUpload" class="hidden" />
        </label>
        {#if !fileInput}
        <button disabled class="transition-all duration-300 absolute mt-52 p-2 px-[5rem] text-black/20 rounded border-[#0569FF]/20 border">Upload</button>
        {:else}
        <button on:click={uploadFile} class="transition-all duration-300 absolute mt-52 p-2 px-[5rem] rounded border-[#0569FF] border hover:bg-[#0569FF] hover:text-white">Upload</button>
        {/if}
    </div>
</div>

<Info />