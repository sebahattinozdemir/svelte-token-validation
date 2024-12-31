<script>
    let telegramId = '';
    let password = '';
    let inputToken = '';
    let showTokenBox = false;
    let userData = {};
  
    // Handle login
    function login() {
      const savedUserData = localStorage.getItem('userData');
      if (!savedUserData) {
        alert('No user found. Please sign up first.');
        window.location.href = '/'; // Redirect to Sign-Up page if no user found
        return;
      }
  
      userData = JSON.parse(savedUserData);
  
      if (userData.telegramID === telegramId && userData.password === password) {
        showTokenBox = true; // Show the token input box after valid login
      } else {
        alert('Invalid Telegram ID or password.');
      }
    }
  
    // Handle token validation
    function validateToken() {
      if (inputToken === userData.token) {
        // Set session as logged in
        localStorage.setItem('isLoggedIn', 'true');
        alert('Successfully logged in! Redirecting to profile...');
        window.location.href = '/profile'; // Redirect to profile page
      } else {
        alert('Invalid token. Redirecting to Sign-Up page.');
        window.location.href = '/'; // Redirect to Sign-Up page if token is invalid
      }
    }
  </script>
  
  <main class="min-h-screen bg-gray-100 flex items-center justify-center">
    <div class="bg-white p-8 rounded-lg shadow-md w-full max-w-md">
      <h1 class="text-2xl font-bold mb-6 text-center">Login</h1>
  
      {#if !showTokenBox}
        <form on:submit|preventDefault={login}>
          <div class="mb-4">
            <label for="telegramId" class="block text-sm font-medium text-gray-700">Telegram ID</label>
            <input type="text" id="telegramId" bind:value={telegramId} class="mt-1 block w-full p-2 border border-gray-300 rounded-md" required />
          </div>
  
          <div class="mb-4">
            <label for="password" class="block text-sm font-medium text-gray-700">Password</label>
            <input type="password" id="password" bind:value={password} class="mt-1 block w-full p-2 border border-gray-300 rounded-md" required />
          </div>
  
          <button type="submit" class="w-full bg-blue-500 text-white py-2 rounded-md hover:bg-blue-600">Log In</button>
        </form>
      {/if}
  
      {#if showTokenBox}
        <div class="bg-yellow-100 border border-yellow-400 text-yellow-700 px-4 py-3 rounded mb-4">
          <p>Enter your previously generated token:</p>
          <input type="text" bind:value={inputToken} placeholder="Authorization Token" class="mt-1 block w-full p-2 border border-gray-300 rounded-md" />
          <button on:click={validateToken} class="w-full bg-green-500 text-white py-2 mt-4 rounded-md hover:bg-green-600">Submit Token</button>
        </div>
      {/if}
    </div>
  </main>
  