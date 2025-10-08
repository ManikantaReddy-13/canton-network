# Canton Network Daml Example

This project demonstrates a simple Daml smart contract workflow for asset transfer using the Canton network and Daml JSON API.

## Project Structure
- `daml/` — Daml source code (see `Main.daml` for the Asset template and script)
- `daml.yaml` — Daml project configuration
- `create.json` — Example payload for creating an Asset contract via the JSON API
- `json-api-app.conf` — Configuration for the Daml JSON API application
- `log/` — Logs for Canton and related services

## Prerequisites
- [Daml SDK](https://docs.daml.com/getting-started/installation.html)
- Java JDK 8 or later (e.g., OpenJDK 11)
- Canton or Daml Sandbox
- [Git](https://git-scm.com/)

## Build and Run
1. **Build the Daml project:**
   ```sh
   daml build
   ```
2. **Start the ledger (Sandbox or Canton):**
   ```sh
   daml sandbox --wall-clock-time --dar ./.daml/dist/json-tests-0.0.1.dar
   ```
3. **Start the JSON API:**
   ```sh
   daml json-api --config json-api-app.conf
   ```
4. **Create an Asset contract via API:**
   - Set your JWT token for Alice:
     ```sh
     export ALICE_JWT=<your-alice-jwt-token>
     ```
   - Run:
     ```sh
     curl -H "Content-Type: application/json" \
          -H "Authorization: Bearer $ALICE_JWT" \
          -d @create.json \
          -X POST localhost:7575/v1/create | jq
     ```

## Notes
- Update `create.json` with the correct `templateId` and parties as needed.
- If you see authentication errors, ensure your JWT is valid and the JSON API is running.
- For GitHub setup, use a Personal Access Token for authentication.

## License
MIT
