# Setting Up Your models.json Config File

Pi needs to know which AI providers and models it can use. You configure this with a models.json file. If you ask Claude to generate this for you based on the Pi docs, it'll produce something like the following — pointing to three free OpenRouter models:

```
{
  "providers": [
    {
      "name": "openrouter",
      "apiKey": "$OPENROUTER_API_KEY",
      "baseUrl": "https://openrouter.ai/api/v1"
    }
  ],
  "models": [
    { "provider": "openrouter", "id": "meta-llama/llama-3.3-70b-instruct:free" },
    { "provider": "openrouter", "id": "google/gemini-2.0-flash-exp:free" },
    { "provider": "openrouter", "id": "mistralai/devstral-small:free" }
  ]
}
```

Notice that apiKey references $OPENROUTER_API_KEY as an environment variable rather than hardcoding your actual key. This is the right approach — it keeps your credentials out of config files and version control.

If Pi launches at this point but shows a “no models available” warning, don’t worry — that just means the OPENROUTER_API_KEY environment variable hasn't been exported yet. That's exactly what you'll fix next.

# Making Your API Key Permanent with .zshrc

```
echo 'export OPENROUTER_API_KEY=sk-or-v1-your-key-here' >> ~/.zshrc
source ~/.zshrc
```