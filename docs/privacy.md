# Privacy & Security

This dashboard was built with strong privacy principles:

- No external analytics or tracking
- No data leaves your browser except:
  - Price requests to Finnhub (only tickers you add)
  - One-time FX rate request to Frankfurter
- API key is stored locally and only sent to Finnhub
- Encrypted backups use PBKDF2 + AES-GCM
- PIN lock is client-side only (deters casual access)

**For maximum security**: Host it on your own hardware behind authentication and use strong backup passwords.
