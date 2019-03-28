# Jumblr

The following RPC calls interact with the `komodod` software, and are made available through the `komodo-cli` software.

## Basic Instructions

- Install Komodo following the [installation guides](../installations/basic-instructions.html#installing-basic-komodo-software) and change into the `komodod` subdirectory using:

```bash
cd ~/komodo/src
```

- Start the daemon:

```bash
./komodod &
```

- Designate a KMD address with at least 10.024 KMD funds:

```bash
./komodo-cli jumblr_deposit KMD_address
```

::: tip
The jumblr process continues until there are less than ~ 10.024 KMD in the deposit address.
:::

- Designate a destination address for your funds. This should be a transparent address that you are keeping secret:

```bash
komodo-cli jumblr_secret destination_KMD_address
```

- Leave your node running until the balance in your first address reaches below 10.024 KMD and the destination address receives the correct amount.

::: warning
Jumblr is created to be resistant against time-based analysis. Because of this, Jumblr is purposefully designed not to be fast. You will need to leave your node running for several hours for the process to finish.
:::

For a more detailed description of Jumblr, please read Section IV of our [whitepaper](https://komodoplatform.com/whitepaper).

#### :pushpin: Examples:

Designate your deposit address.

```bash
./komodo-cli jumblr_deposit RT4mSUjG35QeuGcedsfpHtP5MhDeEGTAqb
```

Designate your secret destination address.

```bash
./komodo-cli jumblr_secret RS46GZ5iTkt2exdauQG3JJ8fdnZNJUvAc1
```

## jumblr_deposit

**jumblr_deposit "depositaddress"**

The `jubmlr_deposit` method indicates the address from which Jumblr should withdraw funds. There should be at least 10.024 KMD in this address. Jumblr will withdraw funds in increments of 10, 100, or 7770 KMD.

::: tip
While shielded z_address technology is available on all KMD-based asset chains, the Jumblr engine and methods are only available on the KMD mainnet.
:::

### Arguments:

| Structure        | Type               | Description                                       |
| ---------------- | ------------------ | ------------------------------------------------- |
| "depositaddress" | (string, required) | the address from which Jumblr will withdraw funds |

### Response:

| Structure | Type | Description |
| --------- | ---- | ----------- |
| (none)    |      |             |

#### :pushpin: Examples:

Command:

```bash
./komodo-cli jumblr_deposit RT4mSUjG35QeuGcedsfpHtP5MhDeEGTAqb
```

Response:

```bash
(none)
```

## jumblr_pause

**jumblr_pause**

The `jumblr_pause` method instructs Jumblr to temporarily pause the privacy-shielding process.

::: tip
See also <b>jumblr_resume</b>.
:::

### Arguments:

| Structure | Type | Description |
| --------- | ---- | ----------- |
| (none)    |      |             |

### Response:

| Structure | Type | Description |
| --------- | ---- | ----------- |
| (none)    |      |             |

#### :pushpin: Examples:

Command:

```bash
./komodo-cli jumblr_pause
```

Response:

```bash
(none)
```

## jumblr_resume

**jumblr_resume**

The `jumblr_resume` method instructs Jumblr to resume the privacy-shielding process.

::: tip
See also <b>jumblr_pause</b>.
:::

### Arguments:

| Structure | Type | Description |
| --------- | ---- | ----------- |
| (none)    |      |             |

### Response:

| Structure | Type | Description |
| --------- | ---- | ----------- |
| (none)    |      |             |

#### :pushpin: Examples:

Command:

```bash
./komodo-cli jumblr_resume
```

Response:

```bash
(none)
```

## jumblr_secret

**jumblr_secret "secretaddress"**

The `jumblr_secret` method indicates to Jumblr the final t destination address. This should be a separate t address that has no connection to the `wallet.dat` file of your `jumblr_deposit` address. Ideally, you should only access the final `jumblr_secret` address via a separate node, and with other layers of privacy (VPN, Tor, etc.).

### Arguments:

| Structure       | Type               | Description                         |
| --------------- | ------------------ | ----------------------------------- |
| "secretaddress" | (string, required) | the destination transparent address |

### Response:

| Structure | Type | Description |
| --------- | ---- | ----------- |
| (none)    |      |             |

#### :pushpin: Examples:

Command:

```bash
./komodo-cli jumbr_secret "RCpMUZwxc3pWsgip5aj3Sy1cKkh86P3Tns"
```

Response:

```bash
(none)
```
