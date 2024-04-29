# Script Exaplained 

if [[ -z $1 ]]; then
# This line starts an if-statement. It checks if the first argument to the script ($1) is empty or not provided.

	echo -e "\n\t Usage: ./Alarm.sh 8h for 8 hours of sleep"
# If the first argument is empty, this line prints a usage message to the console, explaining how to use the script to set an alarm for a specific duration of sleep.
	echo -e "\t\t./Alarm.sh 20m for 20 minutes of sleep"
# This line adds another example to the usage message, demonstrating how to set an alarm for a specific duration in minutes.
	echo -e "\t\t See man sleep\n"
# This line adds a reminder to consult the manual (man sleep) for more information on how to use the sleep command.
	exit 0
# his line exits the script with a status code of 0, indicating successful execution of the script's purpose (displaying the usage message in this case).
fi
# This line marks the end of the if-statement block.

sleep "$1";
# This line pauses the execution of the script for the duration specified by the first argument ($1). For example, if $1 is "8h", it will sleep for 8 hours.
figlet "sleep time over"
# After the sleep duration is over, this line displays the message "sleep time over" using the figlet command, which creates ASCII art text.

alarm=(
# This line defines an array named alarm containing the filenames of different alarm sounds.
	"alarm1.mp3"
	"alarm2.mp3"
	"alarm3.mp3"
	"alarm4.mp3"
	"alarm5.mp3"
)

for ((i=0; i<${#alarm[@]}; i++)); do
# This line starts a for loop that iterates over the elements of the alarm array. It initializes the loop variable i to 0, and the loop continues as long as i is less than the length of the alarm array ${#alarm[@]}.
  figlet -f slant "Wake Up-$((i+1))"
# Inside the loop, this line uses the figlet command to display the message "Wake Up-" followed by the current value of i incremented by 1. This creates a series of messages like "Wake Up-1", "Wake Up-2", and so on.
  sleep 1; mpv --no-audio-display --no-resume-playback "${alarm[i]}" &
# After displaying the "Wake Up" message, this line pauses the script execution for 1 second and then plays the corresponding alarm sound specified by the alarm array at index i using the mpv command. The & at the end runs the command in the background.
  sleep 45; killall mpv
# After playing the alarm sound, this line pauses the script execution for 45 seconds and then terminates any running mpv processes using the killall command. This is to stop the alarm sound after a certain duration.
  sleep 5m;
# After terminating the mpv process, this line makes the script sleep for 5 minutes before proceeding to the next iteration of the loop.
done
# This line marks the end of the for loop block.
