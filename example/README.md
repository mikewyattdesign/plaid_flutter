## Usage Example

``` dart
import 'package:plaid_flutter/plaid_flutter.dart';

class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {

  PlaidLink _plaidLink;
  
  @override
  void initState() {
    super.initState();
  
    _plaidLink = PlaidLink(
      clientName: "CLIENT_NAME",        //required
      publicKey: "PUBLIC_KEY",          //required
      oauthRedirectUri: "myapp://test", //required for android
      oauthNonce: "XXXXXXXXXXXXXXXX",   
      env: EnvOption.sandbox,
      products: <ProductOption>[
        ProductOption.auth,
      ],
      onAccountLinked: (publicToken, metadata) { print("onAccountLinked: $publicToken metadata: $metadata"); },
      onAccountLinkError: (error, metadata) { print("onAccountError: $error metadata: $metadata"); },
      onEvent: (event, metadata) { print("onEvent: $event metadata: $metadata"); },
      onExit: (metadata) { print("onExit: $metadata"); },
    );
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        body: 
        Center( 
            child: 
            RaisedButton(
              onPressed: () {
                _plaidLink.open();
              },
              child: Text("Open Plaid Link"),
          	),
        ),
      ),
    );
  }
}
```