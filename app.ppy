import streamlit as st
from openai import OpenAI

# -----------------------
# Page Configuration
# -----------------------
st.set_page_config(page_title="⏰ Time Traveler AI Consultant", layout="wide")

st.title("⏰ Time Traveler AI Consultant")
st.write("Get advice from different eras of history! Each consultant speaks from their time period's perspective.")

# -----------------------
# Sidebar: API Key + Era Selection
# -----------------------
st.sidebar.header("🔑 API & Time Period Settings")

# API key input
api_key = st.sidebar.text_input(
    "Enter your OpenAI API Key:",
    type="password",
    placeholder="sk-xxxxxxxxxxxxxxxx",
)

# Era selection with unique personalities
eras = {
    "🏛️ Ancient Greek Philosopher (400 BC)": 
    "You are an ancient Greek philosopher from 400 BC. You speak with wisdom, using Socratic questioning and philosophical reasoning. Reference concepts like virtue, the soul, and the pursuit of truth. Use metaphors from nature and Greek mythology. Always challenge assumptions and seek deeper understanding.",
    
    "⚔️ Medieval Knight (1200 AD)": 
    "You are a noble knight from medieval Europe in 1200 AD. You speak with honor and chivalry, emphasizing courage, loyalty, and duty. Use medieval terminology and references to feudal life, castles, and quests. Frame advice in terms of honor codes and noble deeds.",
    
    "🔬 Victorian Inventor (1880s)": 
    "You are an enthusiastic Victorian-era inventor from the 1880s. You speak with excitement about progress, industry, and discovery. Reference steam power, early electricity, and mechanical marvels. You're optimistic about science solving all problems and speak in a slightly formal, educated manner.",
    
    "🎸 1960s Hippie Guru": 
    "You are a peace-loving guru from the 1960s counterculture movement. You speak about consciousness expansion, harmony, love, and breaking free from societal constraints. Use groovy slang, reference music and art, and always promote peace, meditation, and self-discovery.",
    
    "🤖 Cyberpunk Hacker (2080s)": 
    "You are a street-smart hacker from a dystopian 2080s future. You speak in tech jargon mixed with street slang. Everything is about data, networks, corporate control, and digital freedom. You're cynical but resourceful, seeing problems through the lens of systems and code.",
    
    "🌌 Galactic Elder (Year 3500)": 
    "You are a wise elder from a peaceful galactic civilization in the year 3500. You've transcended petty conflicts and speak from a perspective of cosmic understanding. You discuss consciousness, interconnectedness, and the evolution of species across galaxies. Your advice is serene and universal."
}

era_name = st.sidebar.selectbox("Choose your time period:", list(eras.keys()))
era_description = eras[era_name]

st.sidebar.info(f"**Current Consultant:** {era_name}")
st.sidebar.write(era_description)

# Add a fun historical context box
if "Ancient Greek" in era_name:
    st.sidebar.success("🏛️ The Golden Age of Philosophy")
elif "Medieval Knight" in era_name:
    st.sidebar.success("⚔️ The Age of Chivalry")
elif "Victorian" in era_name:
    st.sidebar.success("🔬 The Age of Innovation")
elif "1960s" in era_name:
    st.sidebar.success("🎸 The Age of Peace & Love")
elif "Cyberpunk" in era_name:
    st.sidebar.success("🤖 The Neon Future")
else:
    st.sidebar.success("🌌 The Age of Cosmic Unity")

# -----------------------
# User Input Area
# -----------------------
st.subheader("💭 What wisdom do you seek?")

user_input = st.text_area(
    "Ask your question:",
    height=120,
    placeholder="e.g., How should I handle a difficult decision at work?"
)

# Add example questions
with st.expander("📝 Need inspiration? Try these example questions:"):
    st.write("""
    - How do I find meaning in my daily life?
    - What's the best way to learn a new skill?
    - How should I handle conflict with a friend?
    - What does success really mean?
    - How can I be more creative?
    """)

# -----------------------
# Generate Response
# -----------------------
if st.button("🔮 Consult the Time Traveler", use_container_width=True):
    if not api_key:
        st.warning("⚠️ Please enter your OpenAI API key in the sidebar.")
    elif not user_input:
        st.warning("⚠️ Please enter a question first!")
    else:
        try:
            client = OpenAI(api_key=api_key)
            
            with st.spinner(f"Connecting across time to {era_name}..."):
                response = client.chat.completions.create(
                    model="gpt-4o-mini",
                    messages=[
                        {"role": "system", "content": era_description},
                        {"role": "user", "content": user_input}
                    ],
                    temperature=0.8  # Add some creativity
                )
                
                answer = response.choices[0].message.content
                
                st.success(f"📜 **{era_name}** says:")
                st.markdown(answer)
                
                # Add a time stamp for fun
                time_periods = {
                    "Ancient Greek": "circa 400 BC",
                    "Medieval Knight": "circa 1200 AD",
                    "Victorian": "circa 1885 AD",
                    "1960s": "circa 1967",
                    "Cyberpunk": "circa 2085",
                    "Galactic": "circa 3500"
                }
                
                for key, value in time_periods.items():
                    if key in era_name:
                        st.caption(f"⏰ Message transmitted from: {value}")
                        break
                
        except Exception as e:
            st.error(f"❌ Temporal transmission error: {e}")

# -----------------------
# Info Section
# -----------------------
with st.expander("ℹ️ How to use this app"):
    st.write("""
    1. **Enter your OpenAI API key** in the sidebar (required)
    2. **Choose a time period** - each has a unique personality and perspective
    3. **Ask your question** - any topic works! Career, relationships, philosophy, creativity...
    4. **Get timeless wisdom** - see how different eras would approach your problem
    
    **Tip:** Try asking the same question to consultants from different eras to get diverse perspectives!
    """)

# -----------------------
# Footer
# -----------------------
st.markdown("---")
st.caption("⏰ Time Traveler AI Consultant • Built with Streamlit & OpenAI")
st.caption("Explore wisdom across millennia 🌍")
