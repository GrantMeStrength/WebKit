# WebKit
Using the new (In 2022) WebKit view in iOS. Storing this here so I remember it!

Back story: I used UIWebKit a lot in an app, but Xcode was getting more and more cross about it.
Only issue is that WebKit doesn't have the delegate calls for when a web page loads, or fails.
Turns out you meed to use a new class, WKNavigationDelegate, for that. And then it works great.

```

//
//  ViewController.h
//  testWebKit
//
//  Created by John Kennedy on 2/2/22.
//

#import <UIKit/UIKit.h>
#import <WebKit/WebKit.h>

@interface ViewController  : UIViewController <WKNavigationDelegate>


@end

  -----
  
  
//
//  ViewController.m
//  testWebKit
//
//  Created by John Kennedy on 2/2/22.
//

#import "ViewController.h"


@interface ViewController ()

@property (strong, nonatomic) IBOutlet WKWebView *webview;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    
    _webview.navigationDelegate = self; // If this errors out, make sure you've added  <WKNavigationDelegate> to interface declaration
    
    [_webview loadRequest:[NSMutableURLRequest requestWithURL:[NSURL URLWithString:@"http://www.googleclunkclinck.com"]]];
}

-(void) webView:(WKWebView *)webView didCommitNavigation:(WKNavigation *)navigation {
    NSLog(@"Start");
}

- (void) webView:(WKWebView *)webView didFinishNavigation:(WKNavigation *)navigation {
    NSLog(@"Loaded");
}

-(void) webView:(WKWebView *)webView didFailNavigation:(WKNavigation *)navigation withError:(NSError *)error {
    NSLog(@"Bad things 1");
}
-(void) webView:(WKWebView *)webView didFailProvisionalNavigation:(WKNavigation *)navigation withError:(NSError *)error {
    NSLog(@"Bad things 2");
}
```


@end

  
  
