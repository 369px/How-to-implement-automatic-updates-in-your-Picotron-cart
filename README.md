#How to implement automatic updates in your Picotron cart
Watch the video tutorial: [https://www.youtube.com/watch?v=88nRTLXdAGs](https://www.youtube.com/watch?v=88nRTLXdAGs)

```lua
--define a cart_id_number int where you store your current bbs ID version,
--you can find it in your bbs post like this [cart-5]

function isLatestVersion() --true if latest, else false

  cartName = "YOUR-CART-NAME-ID"
  --change cartName to your cart's name ID without the number

  cartURL = "https://www.lexaloffle.com/bbs/cart_info.php?cid="..cartName.."-"
  local newV = fetch(cartURL..cart_id_number + 1 ) -- +1 cause we want the next one 
  local strToFind = "missing cart_id" 
	
  if not newV then return true
  --if no page is fecthed... return true cause we don't need to update 
  else return string.find(newV, strToFind) ~= nil  end
  --elsif next version's page (fecthed in newV) contains strTofind, there is no new version!

end
```

```lua
function loadUpdate()
  --depending on your case, you may need to back-up what's in ram and load it back in later
  backupUserCart() --just a cp("/ram/cart","/ram/compost/user_cart.p64")
  run_terminal_command("load #phone") --include "terminal.lua" to run this!

  for i=1,39 do 
    flip()
    notify("Loading new update "..i.."/39")
  end 
		
  notify("Update loaded!")
		
  --then you can do whatever you want, install it or just run it
end
```
