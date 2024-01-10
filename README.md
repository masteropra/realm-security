import org.bukkit.Bukkit;
import org.bukkit.ChatColor;
import org.bukkit.command.Command;
import org.bukkit.command.CommandSender;
import org.bukkit.entity.Player;
import org.bukkit.event.EventHandler;
import org.bukkit.event.Listener;
import org.bukkit.event.player.PlayerJoinEvent;
import org.bukkit.event.player.PlayerLoginEvent;
import org.bukkit.plugin.java.JavaPlugin;

import java.util.HashMap;
import java.util.Map;

public class RealmSecurityPlugin extends JavaPlugin implements Listener {

    private Map<Player, Boolean> playerLoggedIn = new HashMap<>();
    private Map<Player, String> playerPasswords = new HashMap<>();

    @Override
    public void onEnable() {
        getServer().getPluginManager().registerEvents(this, this);
    }

    @Override
    public boolean onCommand(CommandSender sender, Command cmd, String label, String[] args) {
        if (cmd.getName().equalsIgnoreCase("login")) {
            // ... (unchanged code for the login command)
        } else if (cmd.getName().equalsIgnoreCase("logout")) {
            // ... (unchanged code for the logout command)
        } else if (cmd.getName().equalsIgnoreCase("changepassword")) {
            // ... (unchanged code for the changepassword command)
        } else if (cmd.getName().equalsIgnoreCase("register")) {
            // ... (unchanged code for the register command)
        } else if (cmd.getName().equalsIgnoreCase("whoami")) {
            // ... (unchanged code for the whoami command)
        } else if (cmd.getName().equalsIgnoreCase("broadcast")) {
            if (sender instanceof Player && sender.isOp()) {
                if (args.length > 0) {
                    String message = String.join(" ", args);
                    Bukkit.broadcastMessage(ChatColor.GREEN + "[Broadcast] " + ChatColor.RESET + message);
                } else {
                    sender.sendMessage("Usage: /broadcast <message>");
                }
                return true;
            } else {
                sender.sendMessage("You do not have permission to use this command.");
                return true;
            }
        } else if (cmd.getName().equalsIgnoreCase("kick")) {
            if (sender instanceof Player && sender.isOp()) {
                if (args.length > 0) {
                    Player target = Bukkit.getPlayer(args[0]);
                    if (target != null) {
                        target.kickPlayer("You have been kicked from the server.");
                    } else {
                        sender.sendMessage("Player not found.");
                    }
                } else {
                    sender.sendMessage("Usage: /kick <player>");
                }
                return true;
            } else {
                sender.sendMessage("You do not have permission to use this command.");
                return true;
            }
        } else if (cmd.getName().equalsIgnoreCase("ban")) {
            if (sender instanceof Player && sender.isOp()) {
                if (args.length > 0) {
                    Player target = Bukkit.getPlayer(args[0]);
                    if (target != null) {
                        Bukkit.getBanList(org.bukkit.BanList.Type.NAME).addBan(target.getName(), "You have been banned from the server.", null, null);
                        target.kickPlayer("You have been banned from the server.");
                    } else {
                        sender.sendMessage("Player not found.");
                    }
                } else {
                    sender.sendMessage("Usage: /ban <player>");
                }
                return true;
            } else {
                sender.sendMessage("You do not have permission to use this command.");
                return true;
            }
        } else if (cmd.getName().equalsIgnoreCase("onlineplayers")) {
            if (sender instanceof Player && sender.isOp()) {
                for (Player onlinePlayer : Bukkit.getOnlinePlayers()) {
                    sender.sendMessage(onlinePlayer.getName());
                }
                return true;
            } else {
                sender.sendMessage("You do not have permission to use this command.");
                return true;
            }
        }
        return false;
    }

    // ... (unchanged code for login event and join event)
}
