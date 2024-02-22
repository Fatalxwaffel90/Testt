import pygame

pygame.init()
screen_width = 800
screen_height = 600
screen = pygame.display.set_mode((screen_width, screen_height))
pygame.display.set_caption("Pong")

# Initialize ball and paddles
ball = pygame.Rect(screen_width // 2, screen_height // 2, 10, 10)
paddle1 = pygame.Rect(10, screen_height // 2 - 30, 10, 60)
paddle2 = pygame.Rect(screen_width - 20, screen_height // 2 - 30, 10, 60)

# Set ball speed and direction
ball_speed_x = 5
ball_speed_y = 5
ball_dx = ball_speed_x
ball_dy = ball_speed_y

# Game variables
player1_score = 0
player2_score = 0

# Game loop
running = True
while running:
    # ...
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        # Handle player 1 and 2 paddle movement using appropriate keys
        # ...

    # Move paddles based on input
    paddle1.y += paddle1_movement
    paddle2.y += paddle2_movement

    # ...
    # Update ball position
    ball.x += ball_dx
    ball.y += ball_dy

    # Check for collisions with walls and paddles
    if ball.top <= 0 or ball.bottom >= screen_height:
        ball_dy *= -1
    if ball.colliderect(paddle1) or ball.colliderect(paddle2):
        ball_dx *= -1

    # Check for scoring and reset ball
    if ball.x < 0:
        player2_score += 1
        ball.x = screen_width // 2
        ball.y = screen_height // 2
        ball_dx = ball_speed_x
        ball_dy = ball_speed_y
    if ball.x > screen_width:
        player1_score += 1
        ball.x = screen_width // 2
        ball.y = screen_height // 2
        ball_dx = -ball_speed_x
        ball_dy = ball_speed_y

    # ...
    # Draw game objects
    screen.fill((0, 0, 0))  # Fill screen with black
    pygame.draw.rect(screen, (255, 255, 255), ball)  # Draw white ball
    pygame.draw.rect(screen, (255, 255, 255), paddle1)  # Draw white paddle1
    pygame.draw.rect(screen, (255, 255, 255), paddle2)  # Draw white paddle2
    # Draw score
    font = pygame.font.Font(None, 36)
    player1_score_text = font.render(str(player1_score), True, (255, 255, 255))
    player2_score_text = font.render(str(player2_score), True, (255, 255, 255))
    screen.blit(player1_score_text, (10, 10))
    screen.blit(player2_score_text, (screen_width - 30, 10))

    pygame.display.flip()

pygame.quit()
