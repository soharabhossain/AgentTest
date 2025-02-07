# AgentTest

import base64
import json

def encode_image(image_path):
    """Encodes an image file as a Base64 string."""
    with open(image_path, "rb") as image_file:
        return base64.b64encode(image_file.read()).decode("utf-8")

def generate_agent_response(llm_response, image_path):
    """Creates a structured response combining LLM output and image encoding."""
    encoded_image = encode_image(image_path)
    
    response_payload = {
        "text_response": llm_response,
        "image_base64": encoded_image,
        "image_format": "png"  # Specify the image format (png, jpg, etc.)
    }
    
    return json.dumps(response_payload)

# Example usage
llm_output = "### AI-Generated Insights\nThis is an LLM-generated response with an accompanying image."
image_path = "output_image.png"

agent_response = generate_agent_response(llm_output, image_path)
print(agent_response)  # This JSON can be sent to the orchestrator


