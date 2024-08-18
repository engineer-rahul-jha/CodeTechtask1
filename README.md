import requests
from web3 import Web3
from solcx import compile_source

# Define your Ethereum node URL (or other blockchain node URL)
NODE_URL = "https://mainnet.infura.io/v3/YOUR_INFURA_PROJECT_ID"
web3 = Web3(Web3.HTTPProvider(NODE_URL))

def get_contract_source_code(address):
    # Assuming the contract is on Etherscan
    api_url = f"https://api.etherscan.io/api?module=contract&action=getsourcecode&address={address}&apikey=YourApiKeyToken"
    response = requests.get(api_url)
    source_code = response.json()['result'][0]['SourceCode']
    return source_code

def analyze_smart_contract(source_code):
    compiled_sol = compile_source(source_code)
    contract_interface = compiled_sol['<stdin>:YourContractName']
    
    # Perform static analysis here - placeholder for vulnerability checks
    vulnerabilities = []
    if 'reentrancy' in source_code:
        vulnerabilities.append('Potential reentrancy vulnerability found')
    if 'selfdestruct' in source_code:
        vulnerabilities.append('Potential misuse of selfdestruct')
    
    return vulnerabilities

def check_consensus_mechanism():
    # Basic placeholder for consensus check
    consensus_algorithm = "Proof of Work"  # Placeholder: Modify based on actual blockchain
    if consensus_algorithm == "Proof of Work":
        print("Ensure there is no 51% attack vulnerability.")
    elif consensus_algorithm == "Proof of Stake":
        print("Check the staking protocol security.")
    else:
        print(f"Unknown consensus mechanism: {consensus_algorithm}")
    
    # Placeholder for advanced consensus checks
    # More detailed checks can be added based on consensus type

def analyze_network_infrastructure():
    # Placeholder for network security analysis
    nodes = web3.geth.admin.peers()
    if len(nodes) < 3:
        print("Warning: The network has less than 3 nodes, which might be vulnerable.")
    
    # Additional network checks can be implemented here
    # For example: checking for open ports, DDoS mitigation, etc.

def main():
    contract_address = '0xYourSmartContractAddressHere'
    source_code = get_contract_source_code(contract_address)
    
    vulnerabilities = analyze_smart_contract(source_code)
    if vulnerabilities:
        print("Vulnerabilities found in smart contract:")
        for v in vulnerabilities:
            print(f"- {v}")
    else:
        print("No major vulnerabilities found in smart contract.")

    check_consensus_mechanism()
    analyze_network_infrastructure()

if __name__ == "__main__":
    main()




#In implemantation to 
#install 
using code on cmd
pip install web3
pip install solcx
