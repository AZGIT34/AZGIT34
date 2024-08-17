import pygame
import sys

# Initialize pygame
pygame.init()

# Screen dimensions
screen_width = 800
screen_height = 600

# Colors
white = (255, 255, 255)
black = (0, 0, 0)

# Create the screen
screen = pygame.display.set_mode((screen_width, screen_height))
pygame.display.set_caption("Mouse Scrolling Animation")

# Load an image or create a surface to scroll
scroll_image = pygame.Surface((screen_width, screen_height * 3))
scroll_image.fill((0, 100, 255))  # Fill with a color for simplicity

# Draw some shapes on the surface to demonstrate scrolling
for i in range(50):
    pygame.draw.circle(scroll_image, white, (screen_width // 2, 100 + i * 100), 50)

# Scrolling variables
scroll_y = 0
scroll_speed = 0

# Clock to manage the frame rate
clock = pygame.time.Clock()

# Main loop
while True:
    # Event handling
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()
        elif event.type == pygame.MOUSEBUTTONDOWN:
            if event.button == 4:  # Mouse scroll up
                scroll_speed = 5
            elif event.button == 5:  # Mouse scroll down
                scroll_speed = -5

    # Update the scroll position
    scroll_y += scroll_speed
    scroll_speed *= 0.9  # Add some inertia to the scroll

    # Limit scrolling to the boundaries of the image
    if scroll_y > 0:
        scroll_y = 0
    elif scroll_y < -scroll_image.get_height() + screen_height:
        scroll_y = -scroll_image.get_height() + screen_height

    # Draw everything
    screen.fill(black)
    screen.blit(scroll_image, (0, scroll_y))
    pygame.display.flip()

    # Limit the frame rate to 60 FPS
    clock.tick(60)
