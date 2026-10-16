# Veil — pago privado no rastreable en Stellar testnet

Privacy pool estilo Tornado (depósito fijo de 10 XLM, commitment en Merkle tree Poseidon,
retiro con prueba Groth16 + nullifier). Ver `PRD.md` y `CLAUDE.md`.

## Estado

| Fase | Estado | Detalle |
|------|--------|---------|
| 1 · Circuito | ✅ | `circuits/withdraw.circom` compila (4396 restricciones no lineales), setup Groth16 hecho, prueba real verificada con snarkjs |
| 2 · Contrato | ⏳ | pendiente |
| 3 · Cliente | ⏳ | `client/tree.js` listo (Merkle + Poseidon); `deposit.js` / `withdraw.js` pendientes |
| 4 · Demo | ⏳ | pendiente |

Test vector Poseidon(1,2) (circomlibjs) = `0x115cc0f5e7d690413df64c6b9662e9cf2a3617f2743245519e19607a4417189a` ✅

## Cuentas testnet
- alice (depositante): `GAJJUTIVOWTTHL73PFPSBNSNMJJZY3EFTTLW7VLVP4LDVA4KXGKYRMVX`
- carol (retira):      `GACFTWXM6RWGB5PDVFRCTBC5T3K6MS7NHKXMLGO3JPD6YH7IN6KZ3RLD`
- dave (destinatario): `GDN5MJPTUSOEAMXMFD3LTYIG7JP4Z7UI746YQHLPK4QATSHZPDKGO2GA`

Contract ID: _pendiente_

## Toolchain (Windows)
- `tools/circom.exe` 2.2.3, `tools/stellar.exe` 28.1.0 (no están en PATH: invocar por ruta)
- Rust 1.99.1 + target `wasm32v1-none` en `~/.cargo/bin`
- snarkjs / circomlibjs / @stellar/stellar-sdk vía `npm i` (local)
- Powers of tau: los mirrors públicos de `powersOfTau28_hez_final_16.ptau` devuelven 403, así que se
  generó uno local de 2^14 (`ptau/pot14_final.ptau`, suficiente: el circuito tiene < 2^13 restricciones).
  Es solo para demo; no es una ceremonia real.

## Cómo correr
```bash
npm i
bash scripts/build-circuit.sh   # compila, setup, prueba de ejemplo y verificación
```
Artefactos en `circuits/build/`: `withdraw_js/withdraw.wasm`, `withdraw_final.zkey`,
`verification_key.json`, `proof.json`, `public.json` (prueba de ejemplo para el test del contrato).
