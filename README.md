# JakimSolatWrapper

An Objective-C class for pulling and parsing prayer times from JAKIM e-Solat Portal. Simple and clean implementation that reads the following information from the web:
- Location
- Code
- Prayer Time

## Setting up the wrapper

You need to add libxml2.dylib to your project.

Go to the Project build settings (Project->Edit Project Settings->Build) and find the "Search Paths". In "Header Search Paths" add the following path:

	/usr/include/libxml2

## Example

SampleViewController.h

	#import <UIKit/UIKit.h>
	#import "JakimSolatParser.h"

	@interface SampleViewController : UIViewController <JakimSolatDelegate> {
    		// instance variables
	}

SampleViewController.m

	- (void)viewDidLoad
	{
    		[super viewDidLoad];
   
    		JakimSolatParser *parser = [[JakimSolatParser alloc] initWithCode:@"sgr03"];
    		parser.delegate = self;
    		[parser parse];
	}

	#pragma mark - Jakim solat delegate

	- (void)jakimSolatParser:(JakimSolatParser *)parser didParsePrayerTime:(JakimPrayerTime *)prayerTime
	{
    		NSDateFormatter *dateFormatter = [[NSDateFormatter alloc] init];
    		[dateFormatter setTimeZone:[NSTimeZone timeZoneWithAbbreviation:@"GMT+8"]];
    		[dateFormatter setDateFormat:@"dd-MM-yyyy HH:mm:ss z"];
    
    		NSLog(@"Kawasan = %@", prayerTime.location);
    		NSLog(@"Kod = %@", prayerTime.code);
    		NSLog(@"Imsak = %@", [dateFormatter stringFromDate:prayerTime.imsak]);
    		NSLog(@"Subuh = %@", [dateFormatter stringFromDate:prayerTime.subuh]);
    		NSLog(@"Syuruk = %@", [dateFormatter stringFromDate:prayerTime.syuruk]);
    		NSLog(@"Zohor = %@", [dateFormatter stringFromDate:prayerTime.zohor]);
    		NSLog(@"Asar = %@", [dateFormatter stringFromDate:prayerTime.asar]);
    		NSLog(@"Maghrib = %@", [dateFormatter stringFromDate:prayerTime.maghrib]);
    		NSLog(@"Isyak = %@", [dateFormatter stringFromDate:prayerTime.isyak]);
	}

	- (void)jakimSolatParser:(JakimSolatParser *)parser didFailWithError:(NSError *)error
	{
    		NSLog(@"JakimSolatWrapper : Failed!");
	}

## Available data

Here is a list of the available properties for prayer time objects:

#### JakimPrayerTime

- (`NSString`)`prayerTime.location`
- (`NSString`)`prayerTime.kod`
- (`NSDate`)`prayerTime.imsak`
- (`NSDate`)`prayerTime.subuh`
- (`NSDate`)`prayerTime.syuruk`
- (`NSDate`)`prayerTime.zohor`
- (`NSDate`)`prayerTime.asar`
- (`NSDate`)`prayerTime.maghrib`
- (`NSDate`)`prayerTime.isyak`

## License

Copyright (c) 2012 Wutmedia. 
Author: Sumardi Shukor <sumardi@wutmedia.com>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

1. The above copyright notice and this permission notice shall be included
   in all copies or substantial portions of the Software.

2. This Software cannot be used to archive or collect data such as (but not
   limited to) that of events, news, experiences and activities, for the 
   purpose of any concept relating to diary/journal keeping.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NON INFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.

## Contact

If you use JakimSolatWrapper on your iPhone/iPad/Mac app then please do let me know, I would love to check it out. 

E-mail : <sumardi@wutmedia.com>
Twitter : <http://twitter.com/sumardi>
