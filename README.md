# James-Bot
using Discord.Commands;
using System;
using System.Linq;

namespace JamesBot
{
    public class DiscordBot
    {
        DiscordClient client;
        CommandService commands;

        public DiscordBot() //most code goes in here
        {

            client = new DiscordClient(input =>
                {
                    input.LogLevel = LogSeverity.Info;
                    input.LogHandler = Log;
                });


            client.UsingCommands(input =>
                {
                    input.PrefixChar = '!'; //character that uses bot commands
                    input.AllowMentionPrefix = true; //bot will answer when called
                });

            commands = client.GetService<CommandService>();

            //triggerd commands

            commands.CreateCommand("Hello").Do(async (e) =>
           {
               await e.Channel.SendMessage("World");
           });
           
           commands = client.GetService<CommandService>();

            commands.CreateCommand("play theme music").Do(async (e) =>
            {
                await e.Channel.SendTTSMessage("Domo arigato, Mr. Roboto, domo, domo,Domo arigato, Mr.Roboto, domo, domo");
                await e.Channel.SendTTSMessage("You're wondering who I am (secret secret I've got a secret).Machine or mannequin (secret secret I've got a secret)");
                await e.Channel.SendTTSMessage("I am the modren man! I've got a secret I've been hiding under my skin.My heart is human, my blood is boiling, my brain I.B.M.");
                await e.Channel.SendTTSMessage("So if you see me acting strangely, don't be surprised,I'm just a man who needed someone, and somewhere to hide");
                await e.Channel.SendTTSMessage("To keep me alive, just keep me alive,Somewhere to hide, to keep me alive");
                await e.Channel.SendTTSMessage("I'm not a robot without emotions. I'm not what you see,I've come to help you with your problems, so we can be free,I'm not a hero, I'm not the saviour, forget what you know");
                await e.Channel.SendTTSMessage("I'm just a man whose circumstances went beyond his control");
                await e.Channel.SendTTSMessage("Beyond my control. We all need control,I need control. We all need control");
                await e.Channel.SendTTSMessage("I am the modren man (secret secret I've got a secret,Who hides behind a mask (secret secret I've got a secret");
                await e.Channel.SendTTSMessage("So no one else can see (secret secret I've got a secret),My true identity");
                await e.Channel.SendTTSMessage("Domo arigato, Mr. Roboto, domo...domo,Domo arigato, Mr. Roboto,Domo arigato, Mr. Roboto,");
                await e.Channel.SendTTSMessage("Thank you very much, Mr. Roboto,for doing the jobs that nobody wants to,And thank you very much, Mr. Roboto");
                await e.Channel.SendTTSMessage("For helping me escape just when I needed to,Thank you, thank you, thank you,I want to thank you, please, thank you");
                await e.Channel.SendTTSMessage("The problem's plain to see,Too much technology,Machines to save our lives,Machines dehumanize.");
                await e.Channel.SendTTSMessage("The time has come at last (secret secret I've got a secret),To throw away this mask (secret secret I've got a secret)");
                await e.Channel.SendTTSMessage("Now everyone can see (secret secret I've got a secret)");
                await e.Channel.SendTTSMessage("My true identity... I'm Kilroy! Kilroy! Kilroy! Kilroy!");
            });
            
            //auto trigger commands

            client.MessageReceived += async (s, e) => //tells bot that if a message is recived
            {
                if (!e.Message.IsAuthor) //if its not from the bot
                    if (e.Message.Text.Contains("Good Bot")|| e.Message.Text.Contains("good Bot")||e.Message.Text.Contains("good bot")|| e.Message.Text.Contains("Good bot")) //sets up the trigger word
                    {
                        await e.Channel.SendMessage("James Bot accepts your PRAISE,for James Bot deserves it!"); //send this message
                    }
            };
            
            client.MessageReceived += async (s, e) => //tells bot that if a message is recived
            {
                if (!e.Message.IsAuthor) //if its not from the bot
                    if (e.Message.Text.Contains("James Bot should I") || e.Message.Text.Contains("James Bot should i") || e.Message.Text.Contains("James Bot should")) //set up the trigger word
                    {
                        Random rnd = new Random(); //starts up random generation
                        int todo = 3;//sets value "todo" as 3,each time this code runs "todo" is reset to the value 3
                        todo = rnd.Next(10);//generates a random number between 1-10 and assigns it to value "todo"

                        if (todo == 1)//for example if the number is 1
                            await e.Channel.SendMessage("James Bot thinks you SHOULD do it"); // it sends this message

                        if (todo == 2)
                            await e.Channel.SendMessage("James Bot thinks you SHOULD NOT do it!"); //send this message

                        if (todo == 3)
                            await e.Channel.SendMessage("James Bot is UNSURE,for the idea has many pro's and cons"); //send this message

                        if (todo == 4)
                            await e.Channel.SendMessage("James Bot belives it to be WRONG,but you should STILL do it!"); //send this message

                        if (todo == 5)
                            await e.Channel.SendMessage("How dare you bother James Bot with such things! That is a STUPID course of action!"); //send this message

                        if (todo == 6)
                            await e.Channel.SendMessage("James Bot thinks you should CONSULT someone with more knowledge on the subject BEFORE you proceed."); //send this message

                        if (todo == 7)
                            await e.Channel.SendMessage("James Bot thinks you should do the OPPOSITE of your plan"); //send this message

                        if (todo == 8)
                            await e.Channel.SendMessage("James Bot thinks you should,but be warned for HIGH chance of failure!"); //send this message

                        if (todo == 9)
                            await e.Channel.SendMessage("James Bot belives you should,for it has a HIGH chance of succeeding"); //send this message

                        if (todo == 10)
                            await e.Channel.SendMessage("James Bot belives that you should do it TWICE in a row!"); //send this message
                    }
            };
            
             client.ExecuteAndWait(async () =>
            {
                await client.Connect("", TokenType.Bot); //you need to insert your own bots token into the quotation marks
            });
        }

        private void Log(object sender, LogMessageEventArgs e)
        {
            Console.WriteLine(e.Message);
        }
    }
}
