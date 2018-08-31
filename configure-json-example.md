---

copyright:
  years: 2018
lastupdated: "2018-03-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Network configuration JSON example
The following IBM Blockchain **network configuration JSON** is the complete example
referenced in [Configure the service - Step 1](configure-service.html):

```
{
	"name": "network",
	"x-networkId": "uuid-uuid1",
	"x-type": "hlfv1",
	"x-app-channel": "mychannel",
	"description": "local network connection profile formatted into IBM Blockchain Platform format",
	"version": "1.0.0",
	"client": {
		"organization": "org1"
	},
	"channels": {
		"mychannel": {
			"orderers": [
				"orderer.example.com"
			],
			"peers": {
				"peer0.org1.example.com": {
					"endorsingPeer": true,
          "chaincodeQuery": true,
          "ledgerQuery": true,
          "eventSource": true
				},
				"peer0.org2.example.com": {
					"endorsingPeer": true,
          "chaincodeQuery": true,
          "ledgerQuery": true,
          "eventSource": true
				}
			}
		}
	},
	"organizations": {
		"Org1MSP" : {
			"mspid": "Org1MSP",
			"peers": [
				"peer0.org1.example.com"
			],
			"certificateAuthorities": [
				"ca-org1"
			]
		},
		"Org2MSP": {
			"mspid": "Org2MSP",
			"peers": [
				"peer0.org2.example.com"
			],
			"certificateAuthorities": [
				"ca-org2"
			]
		}
	},
	"orderers": {
		"orderer.example.com": {
			"url": "grpcs://localhost:7050",
			"grpcOptions": {
        "ssl-target-name-override": "orderer.example.com",
        "grpc.http2.keepalive_time": 15
			},
			"tlsCACerts": {
				"pem": "-----BEGIN CERTIFICATE-----\nMIICNDCCAdqgAwIBAgIRAIBOtq8vZiC0+uLSi2MIS4swCgYIKoZIzj0EAwIwZjEL\nMAkGA1UEBhMCVVMxEzARBgNVBAgTCkNhbGlmb3JuaWExFjAUBgNVBAcTDVNhbiBG\ncmFuY2lzY28xFDASBgNVBAoTC2V4YW1wbGUuY29tMRQwEgYDVQQDEwtleGFtcGxl\nLmNvbTAeFw0xNzA0MjIxMjAyNTZaFw0yNzA0MjAxMjAyNTZaMGYxCzAJBgNVBAYT\nAlVTMRMwEQYDVQQIEwpDYWxpZm9ybmlhMRYwFAYDVQQHEw1TYW4gRnJhbmNpc2Nv\nMRQwEgYDVQQKEwtleGFtcGxlLmNvbTEUMBIGA1UEAxMLZXhhbXBsZS5jb20wWTAT\nBgcqhkjOPQIBBggqhkjOPQMBBwNCAARD2rvgyAmhn8hpu82kAjX3QUg2iqCUPEe1\nQ5CzD5MVv/dK5wrRgkcoMhJLe4HPxYbjV3rodm5Pwi5m3zMGkqNQo2kwZzAOBgNV\nHQ8BAf8EBAMCAaYwGQYDVR0lBBIwEAYEVR0lAAYIKwYBBQUHAwEwDwYDVR0TAQH/\nBAUwAwEB/zApBgNVHQ4EIgQg6q3lkIfG2X/PNQ6U83rZ8saSu2bxghSM5YlA3nCt\n6c4wCgYIKoZIzj0EAwIDSAAwRQIhAL5Lgy7jZ2W74L6i0B23a3JD0W8TSYlTcqXb\nRMSXlLIoAiB2glBl0wM/ITn5+tnHOnq2wrIGuYIiNbLK5oq2zf+gtA==\n-----END CERTIFICATE-----"
			}
		}
	},
	"peers": {
		"peer0.org1.example.com": {
			"url": "grpcs://localhost:7051",
			"eventUrl": "grpcs://localhost:7053",
			"grpcOptions": {
        "ssl-target-name-override": "peer0.org1.example.com",
        "grpc.http2.keepalive_time": 15
			},
			"tlsCACerts": {
				"pem": "-----BEGIN CERTIFICATE-----\nMIICSDCCAe6gAwIBAgIRAPnKpS42wlgtHsddm6q+kYcwCgYIKoZIzj0EAwIwcDEL\nMAkGA1UEBhMCVVMxEzARBgNVBAgTCkNhbGlmb3JuaWExFjAUBgNVBAcTDVNhbiBG\ncmFuY2lzY28xGTAXBgNVBAoTEG9yZzEuZXhhbXBsZS5jb20xGTAXBgNVBAMTEG9y\nZzEuZXhhbXBsZS5jb20wHhcNMTcwNDIyMTIwMjU2WhcNMjcwNDIwMTIwMjU2WjBw\nMQswCQYDVQQGEwJVUzETMBEGA1UECBMKQ2FsaWZvcm5pYTEWMBQGA1UEBxMNU2Fu\nIEZyYW5jaXNjbzEZMBcGA1UEChMQb3JnMS5leGFtcGxlLmNvbTEZMBcGA1UEAxMQ\nb3JnMS5leGFtcGxlLmNvbTBZMBMGByqGSM49AgEGCCqGSM49AwEHA0IABLi5341r\nmriGFHCmVTLdgPGpDFRgwgmHSuLayMsGP0yEmsXh3hKAy24f1mjx/t8WT9G2sAdw\nONsPsfKMSCKpaRqjaTBnMA4GA1UdDwEB/wQEAwIBpjAZBgNVHSUEEjAQBgRVHSUA\nBggrBgEFBQcDATAPBgNVHRMBAf8EBTADAQH/MCkGA1UdDgQiBCCiLa81ayqrV5Lq\nU+NfZvzO8dfxqis6K5Lb+/lqRI6iajAKBggqhkjOPQQDAgNIADBFAiEAr8LYCY2b\nq5kNqOUxgHwBa2KTi/zJBR9L3IsTRDjJo8ECICf1xiDgKqZKrAMh0OCebskYwf53\ndooG04HBoqBLvB8Q\n-----END CERTIFICATE-----"
			}
		},
		"peer0.org2.example.com": {
			"url": "grpcs://localhost:8051",
			"eventUrl": "grpcs://localhost:8053",
			"grpcOptions": {
        "ssl-target-name-override": "peer0.org2.example.com",
        "grpc.http2.keepalive_time": 15
			},
			"tlsCACerts": {
				"pem": "-----BEGIN CERTIFICATE-----\nMIICRzCCAe6gAwIBAgIRAO33HJTheTwvBgWroB6JK40wCgYIKoZIzj0EAwIwcDEL\nMAkGA1UEBhMCVVMxEzARBgNVBAgTCkNhbGlmb3JuaWExFjAUBgNVBAcTDVNhbiBG\ncmFuY2lzY28xGTAXBgNVBAoTEG9yZzIuZXhhbXBsZS5jb20xGTAXBgNVBAMTEG9y\nZzIuZXhhbXBsZS5jb20wHhcNMTcwNDIyMTIwMjU2WhcNMjcwNDIwMTIwMjU2WjBw\nMQswCQYDVQQGEwJVUzETMBEGA1UECBMKQ2FsaWZvcm5pYTEWMBQGA1UEBxMNU2Fu\nIEZyYW5jaXNjbzEZMBcGA1UEChMQb3JnMi5leGFtcGxlLmNvbTEZMBcGA1UEAxMQ\nb3JnMi5leGFtcGxlLmNvbTBZMBMGByqGSM49AgEGCCqGSM49AwEHA0IABDoYTXB0\nMj9j+iSUyM1s7bZZVbDmP7tTej0qWNpS1K7PRsQO2hTfSuiwQrzpaTuGJ4UQPYgu\n9mTJKTWyEVWQ2pSjaTBnMA4GA1UdDwEB/wQEAwIBpjAZBgNVHSUEEjAQBgRVHSUA\nBggrBgEFBQcDATAPBgNVHRMBAf8EBTADAQH/MCkGA1UdDgQiBCBGTVUP6b+efYl2\nzfWdGl1HJZj1TAWMNUYxfFxfsN39bjAKBggqhkjOPQQDAgNHADBEAiB2XoqoNSRw\nYzY6sgomVYtidm7HwiXEsqkrThUHasnOugIgejAgkgXWid6WEdFSAUVpEDsRiek4\nnM2KGw+XJ5/pm/Q=\n-----END CERTIFICATE-----"
			}
		}
	},
	"certificateAuthorities": {
		"ca-org1": {
			"url": "https://localhost:7054/api/v1",
			"httpOptions": {
        "verify": false
      },
      "tlsCACerts": {
				"pem": "-----BEGIN CERTIFICATE-----\nMIICSDCCAe6gAwIBAgIRAPnKpS42wlgtHsddm6q+kYcwCgYIKoZIzj0EAwIwcDEL\nMAkGA1UEBhMCVVMxEzARBgNVBAgTCkNhbGlmb3JuaWExFjAUBgNVBAcTDVNhbiBG\ncmFuY2lzY28xGTAXBgNVBAoTEG9yZzEuZXhhbXBsZS5jb20xGTAXBgNVBAMTEG9y\nZzEuZXhhbXBsZS5jb20wHhcNMTcwNDIyMTIwMjU2WhcNMjcwNDIwMTIwMjU2WjBw\nMQswCQYDVQQGEwJVUzETMBEGA1UECBMKQ2FsaWZvcm5pYTEWMBQGA1UEBxMNU2Fu\nIEZyYW5jaXNjbzEZMBcGA1UEChMQb3JnMS5leGFtcGxlLmNvbTEZMBcGA1UEAxMQ\nb3JnMS5leGFtcGxlLmNvbTBZMBMGByqGSM49AgEGCCqGSM49AwEHA0IABLi5341r\nmriGFHCmVTLdgPGpDFRgwgmHSuLayMsGP0yEmsXh3hKAy24f1mjx/t8WT9G2sAdw\nONsPsfKMSCKpaRqjaTBnMA4GA1UdDwEB/wQEAwIBpjAZBgNVHSUEEjAQBgRVHSUA\nBggrBgEFBQcDATAPBgNVHRMBAf8EBTADAQH/MCkGA1UdDgQiBCCiLa81ayqrV5Lq\nU+NfZvzO8dfxqis6K5Lb+/lqRI6iajAKBggqhkjOPQQDAgNIADBFAiEAr8LYCY2b\nq5kNqOUxgHwBa2KTi/zJBR9L3IsTRDjJo8ECICf1xiDgKqZKrAMh0OCebskYwf53\ndooG04HBoqBLvB8Q\n-----END CERTIFICATE-----"
			},
			"registrar": [
				{
						"affiliation": "group1",
						"enrollId": "admin",
						"enrollSecret": "adminpw"
				}
			]
		},
		"ca-org2": {
			"url": "https://localhost:8054/api/v1",
			"httpOptions": {
        "verify": false
      },
      "tlsCACerts": {
				"pem": "-----BEGIN CERTIFICATE-----\nMIICRzCCAe6gAwIBAgIRAO33HJTheTwvBgWroB6JK40wCgYIKoZIzj0EAwIwcDEL\nMAkGA1UEBhMCVVMxEzARBgNVBAgTCkNhbGlmb3JuaWExFjAUBgNVBAcTDVNhbiBG\ncmFuY2lzY28xGTAXBgNVBAoTEG9yZzIuZXhhbXBsZS5jb20xGTAXBgNVBAMTEG9y\nZzIuZXhhbXBsZS5jb20wHhcNMTcwNDIyMTIwMjU2WhcNMjcwNDIwMTIwMjU2WjBw\nMQswCQYDVQQGEwJVUzETMBEGA1UECBMKQ2FsaWZvcm5pYTEWMBQGA1UEBxMNU2Fu\nIEZyYW5jaXNjbzEZMBcGA1UEChMQb3JnMi5leGFtcGxlLmNvbTEZMBcGA1UEAxMQ\nb3JnMi5leGFtcGxlLmNvbTBZMBMGByqGSM49AgEGCCqGSM49AwEHA0IABDoYTXB0\nMj9j+iSUyM1s7bZZVbDmP7tTej0qWNpS1K7PRsQO2hTfSuiwQrzpaTuGJ4UQPYgu\n9mTJKTWyEVWQ2pSjaTBnMA4GA1UdDwEB/wQEAwIBpjAZBgNVHSUEEjAQBgRVHSUA\nBggrBgEFBQcDATAPBgNVHRMBAf8EBTADAQH/MCkGA1UdDgQiBCBGTVUP6b+efYl2\nzfWdGl1HJZj1TAWMNUYxfFxfsN39bjAKBggqhkjOPQQDAgNHADBEAiB2XoqoNSRw\nYzY6sgomVYtidm7HwiXEsqkrThUHasnOugIgejAgkgXWid6WEdFSAUVpEDsRiek4\nnM2KGw+XJ5/pm/Q=\n-----END CERTIFICATE-----"
			},
			"registrar": [
				{
						"affiliation": "group1",
						"enrollId": "admin",
						"enrollSecret": "adminpw"
				}
			]
		}
	}
}
```
