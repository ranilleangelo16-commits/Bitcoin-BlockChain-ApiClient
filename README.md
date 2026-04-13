# Bitcoin-BlockChain-ApiClient
This a JAVA API client for retrieving data from https://blockchain.info. It can be extended by any developers. The design of the client is very OOP. Enjoy it!

## Requirements

Building the API client library requires:
1. Java 1.8+
2. Maven
3. ANGELo08
## Installation

To create the API client library .jar, execute the following command:

### Manual Installation with Maven

The command below generates .jars, which can be manually included to your project.


```shell
mvn clean package
```

### Manual Installation in Local Repo

In order to add the API client dependency to your maven local repository, execute this command:

```shell
mvn clean install
```
Go to the following link to include third parties libraries to your maven local repository [How to include third parties libraries to your local mvn repository](https://www.mkyong.com/maven/how-to-include-library-manully-into-maven-local-repository/)

### Maven users

You can add this dependency to your pom.xml file:

```xml
<dependency>
  <groupId>com.github.mjggodoy</groupId>
  <artifactId>api-bitcoin-java</artifactId>
  <version>1.0.0-SNAPSHOT</version>
</dependency>
```

## Getting Started

```java

public class ApiCallMain {

	public static void main(String[] args) throws IOException, ParseException {
	
		public static void main(String[] args) throws IOException, ParseException {

		// Set parameters. In order to get the bitcoins transactions per second,
		// the parameters to include are
		// the timespan and the rollingAverage, which correspond to 5 weeks and
		// 8 hours, respectively.

		LinkedHashMap<String, String> params = new LinkedHashMap<String, String>();
		params.put("timespan", "5weeks");
		params.put("start", "1551444600");
		params.put("sampled", "true");
		params.put("rollingAverage", "8hours");
		params.put("format", "csv");

		Statistic statistic = new Statistic(params);
		Chart graphic = statistic.getResourcesTransactionPerSecond();
		System.out.println(graphic.toString());

		// Retrieve charts (type=transaction per second).

		String chartype2 = "transactions-per-second";
		Statistic statistic4 = new Statistic(chartype2);
		Chart graphic2 = statistic4.getResourcesTransaction();
		System.out.println(graphic2.toString());

		// The method getStats returns the summary of bitcoin statistics

		Statistic statistic2 = new Statistic();
		Stat stats = statistic2.getStats();
		System.out.println(stats.toString());
		System.out.println("Get difficulty: " + stats.getDifficulty());

		/// The method getPools() retrieves all the mining pools. In this case,
		// the parameter
		// is the timespan that corresponds to 5 days.

		LinkedHashMap<String, String> params2 = new LinkedHashMap<String, String>();
		params2.put("timespan", "5days");

		Statistic statistic3 = new Statistic(params2);
		Pool pool = statistic3.getPools();
		System.out.println(pool.toString().toLowerCase());

		// The method getRateExchanges() returns the market prices for each
		// currency

		UtilMethods util = new UtilMethods();
		LinkedHashMap<String, LinkedHashMap<String, Object>> output3 = new LinkedHashMap<String, LinkedHashMap<String, Object>>();
		ExchangeRate exchange = new ExchangeRate();
		output3 = exchange.getRateExchanges();
		// System.out.println(output3.toString());
		List<Exchange> exchanges = util.returnToExchangeRate(output3);
		System.out.println(exchanges.get(11).getCurrencyValue());

		/// The method getRateExchanges() returns the exchange rates currency X
		// -> bitcoin. The parameters to add are the currency (EUR)
		// and its value. The method returns a float with the ratio of the
		// exchange.

		LinkedHashMap<String, String> params4 = new LinkedHashMap<String, String>();
		params4.put("currency", "EUR");
		params4.put("value", "5000");
		ExchangeRate exchange2 = new ExchangeRate(params4);
		Rate rate = exchange2.getBitcoinExchange();
		System.out.println(rate.toString());

		// Get information from a block with a specific hash

		String hash = "0000000000000bae09a7a393a8acded75aa67e46cb81f7acaa5ad94f9eacd103";
		BlockChainData blockchain = new BlockChainData(hash);
		Block block = blockchain.getBlockDataInformation();

		// Some examples about how to extract from block of the blockchain i ->
		System.out.println("Previous block " + block.getPrev_block());
		System.out.println("Next block " + block.getNext_block().toString());
		System.out.println("Transactions " + block.getTx().toString());
		System.out.println("Block" + block.toString());

		// Get information from a single transaction by providing the hash

		String hashTransaction = "b6f6991d03df0e2e04dafffcd6bc418aac66049e2cd74b80f14ac86db1e3f0da";
		BlockChainData trasnsactionBlock = new BlockChainData(hashTransaction);
		TransactionData transactionData = trasnsactionBlock.getTransactionData();

		// Some examples about how to extract information about the block ->
		System.out.println("Transaction hash " + transactionData.getHash());
		System.out.println("Transaction's weight " + transactionData.getWeight());
		System.out.println("Transactions' inputs" + transactionData.getInputs());
		System.out.println("Transactions' outputs" + transactionData.getOut().toString());
		System.out.println("Transactions" + transactionData.toString());

		/// Retrieve information from a block given its height

		String height = "154595";
		LinkedHashMap<String, String> paramsHeight = new LinkedHashMap<String, String>();
		paramsHeight.put("format", "json");
		BlockChainData trasnsactionBlockHeight = new BlockChainData(paramsHeight, height);
		List<Block> listBlocks = trasnsactionBlockHeight.getBlockInformationfromHeight();
		System.out.println(listBlocks.get(0).getTx().toString());

		// Retrieve information about a bitcoing given its address
		String address = "1AJbsFZ64EpEfS5UAjAfcUG8pH8Jn3rn1F";
		BlockChainData bitcoinAddress = new BlockChainData(address);
		BitcoinInfo bitcoinInfo = bitcoinAddress.getBitcoinInformationFromAddress();
		System.out.println(bitcoinInfo.toString());

		// Array of transactions referring to a bitcoin
		System.out.println("bitcoininfo: " + bitcoinInfo.toString());
		// Total number of Transactions:
		System.out.println("n_tx: " + bitcoinInfo.getN_tx());

		// Get bitcoin's information from multiple addresses
		LinkedHashMap<String, String> paramsAdresses = new LinkedHashMap<String, String>();
		paramsAdresses.put("active", "1A8JiWcwvpY7tAopUkSnGuEYHmzGYfZPiq|1MDUoxL1bGvMxhuoDYx6i11ePytECAk9QK");
		BlockChainData bitcoinTwoAddress = new BlockChainData(paramsAdresses);
		List<Object> multipleAddresses = bitcoinTwoAddress.getBitcoinsMultipleAddresses();
		System.out.println(multipleAddresses.toString());

		// Get information about the unspent outputs
		LinkedHashMap<String, String> paramsAdressOutputs = new LinkedHashMap<String, String>();
		paramsAdressOutputs.put("active", "1MDUoxL1bGvMxhuoDYx6i11ePytECAk9QK|1A8JiWcwvpY7tAopUkSnGuEYHmzGYfZPiq");
		BlockChainData outputSpent = new BlockChainData(paramsAdressOutputs);
		List<UnspentOutput> unspentOutputList = outputSpent.getUnspentOutputs();
		System.out.println(unspentOutputList.toString());

		// Get information about the latest block
		BlockChainData latestBlock = new BlockChainData();
		Block lastblock = latestBlock.getLastBlock();
		System.out.println(lastblock.toString());

		// Get unconfirmed transactions
		LinkedHashMap<String, String> paramsTransactions = new LinkedHashMap<String, String>();
		paramsTransactions.put("format", "json");
		BlockChainData transactions = new BlockChainData(paramsTransactions);
		List<Transaction> unconfirmedTransactions = transactions.getUnconfirmedTransactions();
		System.out.println(unconfirmedTransactions.toString());

		// Get blocks from a specific pool (e.g., Bitclub Network)
		LinkedHashMap<String, String> paramsPools = new LinkedHashMap<String, String>();
		paramsPools.put("format", "json");
		String poolName = "BitClub%20Network";
		BlockChainData blockPool = new BlockChainData(paramsPools, poolName);
		List<Block> blocks = blockPool.getBlocksfromParameter();
		System.out.println(blocks.toString());

		// Get blocks from a specific day (e.g., Bitclub Network)
		LinkedHashMap<String, String> paramsTime = new LinkedHashMap<String, String>();
		paramsTime.put("timespan", "1day");
		paramsTime.put("format", "json");
		BlockChainData blockChain = new BlockChainData(paramsTime);
		List<Block> blocksfromASpecificTime = blockChain.getBlocksfromParameter();
		System.out.println(blocksfromASpecificTime.toString());

		// Get information about the balance
		LinkedHashMap<String, String> paramsBalance = new LinkedHashMap<String, String>();
		paramsBalance.put("active", "1MDUoxL1bGvMxhuoDYx6i11ePytECAk9QK|1A8JiWcwvpY7tAopUkSnGuEYHmzGYfZPiq");
		BlockChainData balance = new BlockChainData(paramsBalance);
		List<Balance> balanceList = balance.getBalance();
		System.out.println(balanceList.toString());

	}
	}
	}

```

## API documentation

Class | Method | HTTP request | Description
------------ | ------------- | ------------- | -------------
*Chart* | [**getResourcesTransactionPerSecond()**](docs/BlockchainCharts&StatisticsApi.md#getResourcesTransactionPerSecond) | **GET** | This method retrieves the number of bitcoins transactions per second. The parameters to include are: 1) timespan or duration of the chart, 2) rollingAverage or duration over which the data should be averaged, 3) start or the datatime when the chart starts (optional), 3)] the format that is in JSON, 4) Sample that limits the number of points.
*Stat* | [**getStats()**](docs/BlockchainCharts&StatisticsApi.md#getStats) | **GET** | This method retrieves the stats which refer to a summary of blocks and transactions. For example, the hash rate, the total fees, the total number of transactions or mined blocks.
*Pool* | [**getPools()**](docs/BlockchainCharts&StatisticsApi.md#getPools) | **GET** | This method retrieves information about the mining pools.
*LinkedHashMap -> List<Exchange>* | [**getRateExchanges()**](docs/Rate.md#getRateExchanges) | **GET** | This method retrieves the value of each existing currency in bitcoins.
*Rate* | [**getBitcoinExchange()**](docs/Rate.md#getBitcoinExchange) | **GET** | This method retrieves a given currency in bitcoins.
*Block* | [**getBlockDataInformation()**](docs/BlockChainData.md#getBlockDataInformation)  | **GET** | This method provides the information related to a block matching with its corresponding hash.
*TransactionData* | [**getTransactionData()**](docs/BlockChainData.md#getTransactionData) | **GET** | This method provides the information from a single transaction with a given hash.
*Chart* | [**getResourcesTransaction()**](docs/BlockChainData.md#getResourcesTransaction) | **GET** | This method retrieves the transactions regarding the parameter chart type that was specified.
List of *Block* | [**getBlockInformationfromHeight()**](docs/BlockChainData.md#getBlockInformationfromHeight) | **GET** | This method retrieves an array of one or more blocks at the height specified as parameter.
*BitcoinInfo* | [**getBitcoinInformationFromAddress()**](docs/BlockChainData.md#getBitcoinInformationFromAddress) | **GET** | This method retrieves bitcoin information from a specified address.
*AddressBitcoin*, *Wallet*, *Transaction* | [**getBitcoinsMultipleAddresses()**](docs/BlockChainData.md#getBitcoinsMultipleAddresses) | **GET** | This method retrieves bitcoin information (List of AddressBitcoin, Wallet, Transaction) putting as parameter multiple addresses.
*UnspentOutput* | [**getUnspentOutputs()**](docs/BlockChainData.md#getUnspentOutputs) | **GET** | This method retrieves information (List of UnspentOutput) about the unspent outputs by providing as parameter the address.
*Block* | [**getLastBlock()**](docs/BlockChainData.md#getLastBlock) | **GET** | This method returns the last generated block of a blockchain. 
*Transaction* | [**getUnconfirmedTransactions()**](docs/BlockChainData.md#getUnconfirmedTransactions) | **GET** | This method returns all the unconfirmed transactions. 
*Block* | [**getBlocksfromParameter()**](docs/BlockChainData.md#getBlocksfromParameter) | **GET** | This method returns the blocks generated for a day or a specific pool (e.g., putting as parameters 1day or BitClub%20Network as mining pool, respectively)
*Balance* | [**getBalance()**](docs/BlockChainData.md#getBalance) | **GET** | Get information about the balance




