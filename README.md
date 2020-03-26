(********************************************************************************
**
** Description:		Setting up the virtual WebCam for ChromaKey
** Author: 			Dennis Wilsmann (dwilsman)
** Confirmed working: 	MacOS 10.15.3+
** Required Apps:		OBS, CamTwist
*********************************************************************************)

(* Start SyphonInject *)
tell application "SyphonInject"
	activate
end tell

(* Start OBS *)
tell application "OBS"
	activate
end tell

(*Start CamTwist *)
tell application "CamTwist"
	activate
end tell

(* Inject Camera Traffic *)
tell application "System Events"
	(*wait for OBS to start*)
	repeat until (window 1 of process "OBS" exists)
		delay 1
	end repeat
	
	(*wait for SyphonInject to start*)
	repeat until (window 1 of process "SyphonInject" exists)
		delay 1
	end repeat
	
	tell process "SyphonInject"
		tell table 1 of scroll area 1 of window "SyphonInject"
			select (row 1 where value of text field 1 is "OBS")
			
		end tell
		click button "Inject" of window "SyphonInject"
	end tell
	
	
	
	(*prepare CamTwist*)
	tell process "CamTwist"
		tell table 1 of scroll area 1 of splitter group 1 of window "Cam Twist"
			select (row 1 where value of text field 1 is "SYP")
		end tell
		click button 5 of window "Cam Twist"
		
		tell pop up button 1 of scroll area 3 of window "Cam Twist"
			click
			tell menu 1
				click menu item "OBS"
			end tell
		end tell
	end tell
	
end tell
