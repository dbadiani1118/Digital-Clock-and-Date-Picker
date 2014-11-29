Digital-Clock-and-Date-Picker
=============================
//
//  ViewController.m
//  myDigitalClock
//
//  Created by Dimple Badiani on 3/3/14.
//  Copyright (c) 2014 Dimple Badiani. All rights reserved.
//

#import "ViewController.h"

@interface ViewController ()

@end

@implementation ViewController

@synthesize stbutton, stobutton, rbutton;

@synthesize display;
@synthesize counterTime;
@synthesize myPicker;

- (void)runTimer {
    
    // This starts the timer which fires the showActivity
    // method every 0.5 seconds
    
    myTicker = [NSTimer scheduledTimerWithTimeInterval: 0.5 target: self selector: @selector(showActivity) userInfo: nil repeats: YES];
    
}


// This method is run every 0.5 seconds by the timer created
// in the function runTimer

- (void)showActivity {
    
    NSDateFormatter *formatter = [[NSDateFormatter alloc] init];
    NSDate *date = [NSDate date];
    
    // This will produce a time that looks like "12:15:00 PM".
    [formatter setTimeStyle:NSDateFormatterMediumStyle];
    
    // This sets the label with the updated time.
    [display setText:[formatter stringFromDate:date]];
    
}



-(void)showTimerActivity;
{
    counterInt += 1;
    
    int hours = counterInt / 3600 ;
    int minutes = counterInt / 60 - hours * 60;
    int seconds = counterInt - hours * 3600 - minutes * 60;
    
    counterTime.text = [NSString stringWithFormat:@"%02d:%02d:%02d", hours, minutes, seconds];
    
    
}


- (IBAction)startButton:(id)sender {
    
    myTicker = [NSTimer scheduledTimerWithTimeInterval:1 target:self selector:@selector(showTimerActivity) userInfo:nil repeats:YES];
    

    
}

- (IBAction)stopButon:(id)sender {
    
    [myTicker invalidate];
    myTicker = nil;
  
    }


- (IBAction)resetButton:(id)sender {
    
    
    counterInt = 0;
    counterTime.text=@"00:00:00";
    
    
    
}

- (IBAction)buttonPressed:(id)sender {
    
    
    
    NSDate *selected =[myPicker date];
    NSString *message =[[NSString alloc] initWithFormat:
                        @"The Date and Time you selected is: %@",selected];
    
    UIAlertView *alert=[[UIAlertView alloc] initWithTitle:@"Date and Time Selected" message:message delegate:nil cancelButtonTitle:@"Yes, I did." otherButtonTitles:nil];
    
    [alert show];
}

- (void)viewDidLoad
{
    
	NSDate *now = [[NSDate alloc] init];
    [myPicker setDate:now animated:YES];
    
    
    [super viewDidLoad];
	
	[self runTimer];
    
    counterInt = 0;
    display.text=@"";
    counterTime.text=@"";
    
    
    
  
    
}

- (void)didReceiveMemoryWarning
{
    [super didReceiveMemoryWarning];
    // Dispose of any resources that can be recreated.
}

@end
