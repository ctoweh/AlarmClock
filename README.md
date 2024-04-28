if [[ -z $1 ]]; then
	echo -e "\n\t Usage: ./Alarm.sh 8h for 8 hours of sleep"
	echo -e "\t\t./Alarm.sh 20m for 20 minutes of sleep"
	echo -e "\t\t See man sleep\n"
	exit 0
fi

# This script checks if the first argument passed to it is empty. 
# If it is empty, it prints usage information and exits. 
# If there is an argument, it continues executing the rest of the script.
# It uses the echo command to print a message to the standard output.
# The -e flag enables interpretation of backslash escapes, allowing for formatting. 
# This line prints a usage message informing the user how to use the script, specifying that they should run ./Alarm.sh followed by a duration in hours or minutes.
# Another example of how to use the script, specifying that they can use minutes instead of hours by providing a duration followed by 'm'.
#  Another message directing the user to refer to the manual page (man) for the sleep command, suggesting they can find more information there.



sleep "$1"; 
# This line uses the sleep command to pause the execution of the script for the duration specified by the first argument passed to the script ($1). The value of $1 is the duration of sleep specified by the user, either in hours or minutes.

figlet "sleep time over"
# This line uses the figlet command to generate ASCII art text that spells out "sleep time over". figlet is a program that generates text banners in a variety of typefaces. Here, it's used to display a message indicating that the sleep time is over.

alarm=(
# This line initializes an array variable named alarm. Arrays in Bash are ordered lists of values. In this case, the array contains the filenames of MP3 files that presumably contain alarm sounds.

	"alarm1.mp3"
	"alarm2.mp3"
	"alarm3.mp3"
	"alarm4.mp3"
	"alarm5.mp3"
 # These are the elements of the alarm array. Each element is a string representing the filename of an MP3 file containing an alarm sound. The script uses these filenames to play an alarm sound to wake the user up after the specified sleep duration.
)

for ((i=0; i<${#alarm[@]}; i++)); do
  figlet -f slant "Wake Up-$((i+1))"
  sleep 1; mpv --no-audio-display --no-resume-playback "${alarm[i]}" &
  sleep 45; killall mpv
  sleep 5m;
done
