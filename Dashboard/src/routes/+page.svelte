<main class="p-24 text-center">
    <div>
        <h1 class="font-bold rounded-sm text-black bg-green-300 w-full p-5 text-xl shadow-sm shadow-black">The following link will guide you to the dashboard.</h1>
        <button class="m-10 bg-rose-500 p-4 w-1/2 text-white font-bold rounded-md shadow-red-800 shadow-sm" on:click={() => {
            window.location.href = "./Dashboard";
        }}>Go To The Dashboard</button>
    </div>
</main>