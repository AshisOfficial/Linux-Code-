# Linux-Code-
#!/bin/bash

# æ£€æŸ¥æ˜¯å¦ä¼ å…¥äº†å‚æ•°
if [ "$#" -ne 1 ]; then
  echo "Usage: $0 <claim_reward_address>"
  exit 1
fi

CLAIM_REWARD_ADDRESS=$1

# ç¬¬ä¸€æ®µå‘½ä»¤ï¼šåˆ é™¤æ—§çš„cysic-verifierç›®å½•ï¼Œåˆ›å»ºæ–°çš„ç›®å½•ï¼Œå¹¶ä¸‹è½½å¿…è¦çš„æ–‡ä»¶
rm -rf ~/cysic-verifier
cd ~
mkdir cysic-verifier
curl -L https://github.com/cysic-labs/cysic-phase3/releases/download/v1.0.0/verifier_linux >~/cysic-verifier/verifier

# ç¬¬äºŒæ®µå‘½ä»¤ï¼šåˆ›å»ºé…ç½®æ–‡ä»¶
cat <<EOF >~/cysic-verifier/config.yaml
# Not Change
chain:
  # Not Change
  endpoint: "grpc-testnet.prover.xyz:80"
  # Not Change
  chain_id: "cysicmint_9001-1"
  # Not Change
  gas_coin: "CYS"
  # Not Change
  gas_price: 10
  # Modify Hereï¼š! Your Address (EVM) submitted to claim rewards
claim_reward_address: "$CLAIM_REWARD_ADDRESS"

server:
  # don't modify this
  cysic_endpoint: "https://ws-pre.prover.xyz"
  verify_endpoint: "http://verifier-rpc.prover.xyz:50052"
EOF

# ç¬¬ä¸‰æ®µå‘½ä»¤ï¼šè®¾ç½®æ‰§è¡Œæƒé™å¹¶å¯åŠ¨verifier
cd ~/cysic-verifier/
chmod +x ~/cysic-verifier/verifier
echo "LD_LIBRARY_PATH=. CHAIN_ID=534352 ./verifier" >~/cysic-verifier/start.sh
chmod +x ~/cysic-verifier/start.sh
