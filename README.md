#include <stdio.h> #include <string.h>
#define MAX_TEAMS 20 #define MAX_NAME_LEN 50 #define MAX_PLAYERS 11
typedef struct {
char name[MAX_NAME_LEN];
char players[MAX_PLAYERS][MAX_NAME_LEN]; int num_players;
} Team;
int main() {
int num_teams;
Team teams[MAX_TEAMS]; int i, j, k;
// Get number of teams and team names printf("Enter the number of teams: "); scanf("%d", &num_teams);
for (i = 0; i < num_teams; i++) {
printf("Enter the name of team %d: ", i+1); scanf("%s", teams[i].name);
printf("Enter the number of players for team %d: ", i+1); scanf("%d", &teams[i].num_players);
for (j = 0; j < teams[i].num_players; j++) { printf("Enter the name of player %d: ", j+1);
scanf("%s", teams[i].players[j]); }
}
// Display team names and player names printf("\n");
for (i = 0; i < num_teams; i++) {
printf("Team %d: %s\n", i+1, teams[i].name); printf("Players: ");
for (j = 0; j < teams[i].num_players; j++) {
printf("%s ", teams[i].players[j]); }
printf("\n\n"); }
// Generate schedule printf("Generating schedule...\n\n"); for (i = 0; i < num_teams-1; i++) {
for (j = i+1; j < num_teams; j++) {
printf("%s vs %s\n", teams[i].name, teams[j].name); }
}
// Update schedule in file
FILE *fptr;
fptr = fopen("schedule.txt", "w");
if (fptr == NULL) {
printf("Error opening file.\n");
return 1; }
fprintf(fptr, "IPL Cricket Tournament Schedule\n\n");
for (i = 0; i < num_teams-1; i++) { for (j = i+1; j < num_teams; j++) {
fprintf(fptr, "%s vs %s\n", teams[i].name, teams[j].name); }
}
fclose(fptr);
return 0; }
