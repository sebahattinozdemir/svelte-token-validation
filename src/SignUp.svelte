<script>
    let telegramId = '';
    let password = '';
    let authToken = '';
    let showAuthToken = false;
    let userData = {}; // Object to store user sign-up data
  
    // Generate token
    function generateToken() {
      return Math.random().toString(36).substr(2) + Math.random().toString(36).substr(2);
    }
  
    // Handle sign up
    function signUp() {
      if (!telegramId || !password) {
        alert('Please fill in all fields.');
        return;
      }
  
      authToken = generateToken();
      userData = {
        telegramID: telegramId,
        password: password,
        createdAt: new Date(),
        token: authToken,
      };
  
      // Save the userData in localStorage to simulate a "database"
      localStorage.setItem('userData', JSON.stringify(userData));
      showAuthToken = true;
    }
  
    function confirmToken() {
      showAuthToken = false;
      alert('Thank you! You have successfully registered.');
      telegramId = '';
      password = '';
    }
  </script>
  
  <main class="min-h-screen bg-gray-100 flex items-center justify-center">
    <div class="bg-white p-8 rounded-lg shadow-md w-full max-w-md">
      <h1 class="text-2xl font-bold mb-6 text-center">Sign Up</h1>
  
      {#if showAuthToken}
        <div class="bg-yellow-100 border border-yellow-400 text-yellow-700 px-4 py-3 rounded mb-4">
          <p><strong>Your authorization token:</strong></p>
          <p class="text-sm break-all bg-gray-200 p-2 rounded">{authToken}</p>
          <p class="text-sm mt-2">Please copy and save it somewhere safe.</p>
          <button on:click={confirmToken} class="w-full bg-green-500 text-white py-2 mt-4 rounded-md hover:bg-green-600">OK</button>
        </div>
      {/if}
  
      {#if !showAuthToken}
        <form on:submit|preventDefault={signUp}>
          <div class="mb-4">
            <label for="telegramId" class="block text-sm font-medium text-gray-700">Telegram ID</label>
            <input type="text" id="telegramId" bind:value={telegramId} class="mt-1 block w-full p-2 border border-gray-300 rounded-md" required />
          </div>
  
          <div class="mb-4">
            <label for="password" class="block text-sm font-medium text-gray-700">Password</label>
            <input type="password" id="password" bind:value={password} class="mt-1 block w-full p-2 border border-gray-300 rounded-md" required />
          </div>
  
          <button type="submit" class="w-full bg-blue-500 text-white py-2 rounded-md hover:bg-blue-600">Sign Up</button>
        </form>
      {/if}
    </div>
  </main>
  